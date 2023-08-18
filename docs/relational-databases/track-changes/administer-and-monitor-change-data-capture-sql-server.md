---
title: "Administer and monitor change data capture"
description: "Learn how to administer and monitor change data capture on SQL Server, Azure SQL Managed Instance, and Azure SQL Database."
author: MikeRayMSFT
ms.author: mikeray
ms.date: 03/16/2023
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "change data capture, monitoring"
  - "change data capture, administering"
  - "change data capture, jobs"
---
# Administer and monitor change data capture 
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

This topic describes how to administer and monitor change data capture.  
  
> [!NOTE]  
> In Azure SQL Database, the capture and cleanup SQL Server Agent jobs are replaced by a change data capture scheduler that invokes stored procedures to start periodic capture and cleanup of the change tables. For more information, see the section on [CDC in Azure SQL Database](#cdc-in-azure-sql-database) later in this article.

## <a name="Capture"></a> Capture job

The capture job is initiated by running the parameterless stored procedure `sp_MScdc_capture_job`. This stored procedure starts by extracting the configured values for `maxtrans`, `maxscans`, `continuous`, and `pollinginterval` for the capture job from `msdb.dbo.cdc_jobs`. These configured values are then passed as parameters to the stored procedure `sp_cdc_scan`. This is used to invoke `sp_replcmds` to perform the log scan. 

In Azure SQL Database, `continuous` and `pollinginterval` parameters do not apply. For more information, see [CDC in Azure SQL Database](#cdc-in-azure-sql-database).
  
### Capture job parameters  

To understand capture job behavior, you must understand how the configurable parameters are used by `sp_cdc_scan`.
  
#### `maxtrans` parameter

The `maxtrans` parameter specifies the maximum number of transactions that can be processed in a single scan cycle of the log. If during the scan the number of transactions to be processed reaches this limit, no additional transactions are included in the current scan. After a scan cycle is complete, the number of transactions that were processed will always be less than or equal to `maxtrans`.

#### `maxscans` parameter

The `maxscans` parameter specifies the maximum number of scan cycles that are attempted to drain the log before either returning (continuous = 0) or executing a waitfor (continuous = 1).

#### `continuous` parameter

The `continuous` parameter controls whether `sp_cdc_scan` relinquishes control in after either draining the log or executing the maximum number of scan cycles (one-shot mode). It also controls whether `sp_cdc_scan` continues to run until explicitly stopped (continuous mode).  
  
##### One-shot mode

In one-shot mode, the capture job requests `sp_cdc_scan` to perform up to `maxtrans` scans to try to drain the log and return. Any transactions in addition to `maxtrans` that are present in the log will be processed in later scans.  
  
 One-shot mode is used in controlled tests, where the volume of transactions to be processed is known, and there are advantages to the fact that the job closes automatically on when it is finished. One-shot mode is not recommended for production use. This is because it relies on the job schedule to manage how frequently the scan cycle is run.  
  
 When running in one-shot mode, you can compute an upper bound on expected throughput of the capture job, expressed in transactions per second by using the following computation:  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 Even if the time that is required to scan the log and populate the change tables were not significantly different from 0, the average throughput of the job could not exceed the value obtained by dividing the maximum allowed transactions for a single scan multiplied by the maximum allowed scans by the number of seconds separating log processing.  
  
 If one-shot mode were to be used to regulate log scanning, the number of seconds between log processing would have to be governed by the job schedule. When this kind of behavior is desired, running the capture job in continuous mode is a better way to reschedule the log scan.  
  
##### Continuous mode and polling interval

In continuous mode, the capture job requests that `sp_cdc_scan` run continuously. This lets the stored procedure manage its own wait loop by providing not only for `maxtrans` and `maxscans` but also a value for the number of seconds between log processing (the polling interval). In continuous mode, the capture job remains active, executing a `WAITFOR` between log scanning.  
  
> [!NOTE]  
> When the value of the polling interval is greater than 0, the same upper limit on throughput for the recurring one-shot job also applies to the job operation in continuous mode. That is, (`maxtrans` \* `maxscans`) divided by a nonzero polling interval will put an upper bound on the average number of transactions that can be processed by the capture job.  
  
### Capture job customization

For the capture job, you can apply additional logic to determine whether a new scan begins immediately or whether a sleep is imposed before it starts a new scan instead of rely on a fixed polling interval. The choice could be based merely on time of the day, perhaps enforcing very long sleeps during peak activity times, and even moving to a polling interval of 0 at close of day when it is important to complete the days processing and prepare for nightly runs. Capture process progress could also be monitored to determine when all transactions committed by midnight had been scanned and deposited in change tables. This lets the capture job end, to be restarted by a scheduled daily restart. To customize behavior, you can replace the job step that calls `sp_cdc_scan` with a call to a user written wrapper for `sp_cdc_scan`.

## <a name="Cleanup"></a> Cleanup job

This section provides information about how the change data capture cleanup job works.  
  
### Structure of the cleanup job

Change data capture uses a retention-based cleanup strategy to manage change table size. In SQL Server and Azure SQL Managed Instance, the cleanup mechanism consists of a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent [!INCLUDE[tsql](../../includes/tsql-md.md)] job that is created when the first database table is enabled. A single cleanup job handles cleanup for all database change tables and applies the same retention value to all defined capture instances.
  
The cleanup job is initiated by running the parameterless stored procedure `sp_MScdc_cleanup_job`. This stored procedure starts by extracting the configured retention and threshold values for the cleanup job from `msdb.dbo.cdc_jobs`. The retention value is used to compute a new low watermark for the change tables. The specified number of minutes is subtracted from the maximum `tran_end_time` value from the `cdc.lsn_time_mapping` table to obtain the new low water mark expressed as a datetime value. The CDC.lsn_time_mapping table is then used to convert this datetime value to a corresponding `lsn` value. If the same commit time is shared by multiple entries in the table, the `lsn` that corresponds to the entry that has the smallest `lsn` is chosen as the new low watermark. This `lsn` value is passed to `sp_cdc_cleanup_change_tables` to remove change table entries from the database change tables.  
  
> [!NOTE]  
> The advantage of using the commit time of the recent transaction as the base for computing the new low watermark is that it lets the changes remain in change tables for the specified time. This happens even when the capture process is running behind. All entries that have the same commit time as the current low watermark continue to be represented within the change tables by choosing the smallest `lsn` that has the shared commit time for the actual low watermark.  

When a cleanup is performed, the low watermark for all capture instances is initially updated in a single transaction. It then tries to remove obsolete entries from the change tables and the cdc.lsn_time_mapping table. The configurable threshold value limits how many entries are deleted in any single statement. Failure to perform the delete on any individual table will not prevent the operation from being attempted on the remaining tables.  
  
### Cleanup job customization

 For the cleanup job, the possibility for customization is in the strategy used to determine which change table entries are to be discarded. The only supported strategy in the delivered cleanup job is a time-based one. In that situation, the new low watermark is computed by subtracting the allowed retention period from the commit time of the last transaction processed. Because the underlying cleanup procedures are based on `lsn` instead of time, any number of strategies can be used to determine the smallest `lsn` to keep in the change tables. Only some of these are strictly time-based. Knowledge about the clients, for example, could be used to provide a failsafe if downstream processes that require access to the change tables cannot run. Also, although the default strategy applies the same `lsn` to clean up all the databases' change tables, the underlying cleanup procedure, can also be called to clean up at the capture instance level.  
 
> [!NOTE]  
> In Azure SQL Database, the change data capture scheduler periodically invokes a stored procedure to capture and cleanup change tables.  As such, the customization of the capture and cleanup process in Azure SQL Database is not currently possible. Though the scheduler runs the stored procedures automatically, it's also possible to start them manually by the user. For more information, see the section on [CDC in Azure SQL Database](#cdc-in-azure-sql-database) later in this doc.


## <a name="Monitor"></a> Monitor the process

Monitoring the change data capture process lets you determine if changes are being written correctly and with a reasonable latency to the change tables. Monitoring can also help you to identify any errors that might occur. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] includes two dynamic management views to help you monitor change data capture: [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) and [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md).  
  
### Identify sessions with empty result sets

Every row in `sys.dm_cdc_log_scan_sessions` represents a log scan session (except the row with an ID of 0). A log scan session is equivalent to one execution of [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md). During a session, the scan can either return changes or return an empty result. If the result set is empty, the empty_scan_count column in `sys.dm_cdc_log_scan_sessions` is set to 1. If there are consecutive empty result sets, such as if the capture job is running continuously, the empty_scan_count in the last existing row is incremented. For example, if `sys.dm_cdc_log_scan_sessions` already contains 10 rows for scans that returned changes and there are five empty results in a row, the view contains 11 rows. The last row has a value of 5 in the empty_scan_count column. To determine sessions that had an empty scan, run the following query:  

```sql
SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0
```

### Determine latency

The `sys.dm_cdc_log_scan_sessions` management view includes a column that records the latency for each capture session. Latency is defined as the elapsed time between a transaction being committed on a source table and the last captured transaction being committed on the change table. The latency column is populated only for active sessions. For sessions with a value greater than 0 in the empty_scan_count column, the latency column is set to 0. The following query returns the average latency for the most recent sessions:  

```sql
SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0
```

You can use latency data to determine how fast or slow the capture process is processing transactions. This data is most useful when the capture process is running continuously. If the capture process is running on a schedule, latency can be high because of the lag between transactions being committed on the source table and the capture process running at its scheduled time.  
  
 Another important measure of capture process efficiency is throughput. This is the average number of commands per second that are processed during each session. To determine the throughput of a session, divide the value in the command_count column by the value in the duration column. The following query returns the average throughput for the most recent sessions:  

```sql
SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0
```

### Use data collector to collect sampling data

The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data collector lets you collect snapshots of data from any table or dynamic management view and build a performance data warehouse. When change data capture is enabled on a database, it is useful to take snapshots of the `sys.dm_cdc_log_scan_sessions` view and the sys.dm_cdc_errors view at regular intervals for later analysis. The following procedure sets up a data collector for collecting sample data from the `sys.dm_cdc_log_scan_sessions` management view.

#### Configuring data collection

1. Enable data collector and configure a management data warehouse. For more information, see [Manage Data Collection](../../relational-databases/data-collection/manage-data-collection.md).  
  
2. Execute the following code to create a custom collector for change data capture.  

    ```sql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  

    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,
    @collection_mode = 0,
    @days_until_expiration = 30,
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from
    -- the change data capture dynamic management view.  
    DECLARE @parameters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @parameters = CONVERT(xml,
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,
    @parameters = @parameters,  
    @collection_item_id = @collection_item_id output;
  
    GO  
    ```  
  
3. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expand **Management**, and then expand **Data Collection**. Right-click **CDC Performance Data Collector**, and then click **Start Data Collection Set**.  
  
4. In the data warehouse you configured in step 1, locate the table custom_snapshots.cdc_log_scan_data. This table provides a historical snapshot of data from log scan sessions. This data can be used to analyze latency, throughput, and other performance measures over time.  

## <a name="ScriptUpgrade"></a> Script upgrade mode

When you apply cumulatives updates or service packs to an instance, at restart, the instance can enter in Script Upgrade mode. In this mode, SQL Server may run a step to analyze and upgrade internal CDC tables, which could result in recreating objects like indexes on capture tables. Depending on the amount of data involved, this step might take some time or cause high transaction log usage for enabled CDC databases.

## CDC in Azure SQL Database

In Azure SQL Database, the same configuration options and objects are not available because the capture and cleanup SQL Server Agent jobs are replaced by a change data capture scheduler. The scheduler invokes stored procedures to start periodic capture and cleanup of the change tables. 

However, some limited customizations are supported.

- The frequency of the CDC capture and cleanup jobs cannot be customized.
- The `pollinginterval` and `continuous` values are not used in Azure SQL DB for capture and cleanup jobs.
- Dropping the capture job entry from the `cdc.cdc_jobs` table doesn't stop the capture job running in the background.
- Dropping the cleanup job causes the cleanup job to not run.
- The `cdc.cdc_jobs` table exists in the `cdc` schema, not `msdb`.

Given those limitations, it is possible to:

- Query the `cdc.cdc_jobs` table for current configuration information.
- Configure the `maxtrans` and `maxscans` options using the `sp_cdc_change_job` stored procedure.
- Drop and add jobs using `sp_cdc_drop_job` and `sp_cdc_add_job`.

## See also

- [Track Data Changes &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)
- [About change data capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)
- [Enable and Disable change data capture &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)
- [Work with Change Data &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
