---
title: Read queries on replicas
titleSuffix: Azure SQL Database & SQL Managed Instance
description: Azure SQL provides the ability to use the capacity of read-only replicas for read workloads, called Read Scale-Out.
author: rajeshsetlem
ms.author: rsetlem
ms.reviewer: wiassaf, mathoma, randolphwest
ms.date: 06/19/2023
ms.service: sql-database
ms.subservice: scale-out
ms.topic: conceptual
ms.custom:
  - sqldbrb=1
  - devx-track-azurepowershell
monikerRange: "= azuresql || = azuresql-db || = azuresql-mi"
---
# Use read-only replicas to offload read-only query workloads

[!INCLUDE[appliesto-sqldb-sqlmi](../includes/appliesto-sqldb-sqlmi.md)]

As part of [High Availability architecture](high-availability-sla.md#locally-redundant-availability), each single database or elastic pool database in the Premium and Business Critical service tier is automatically provisioned with a primary read-write replica and one or more secondary read-only replicas. The secondary replicas are provisioned with the same compute size as the primary replica. The *read scale-out* feature allows you to offload read-only workloads using the compute capacity of one of the read-only replicas, instead of running them on the read-write replica. This way, some read-only workloads can be isolated from the read-write workloads, and don't affect their performance. The feature is intended for the applications that include logically separated read-only workloads, such as analytics. In the Premium and Business Critical service tiers, applications could gain performance benefits using this additional capacity at no extra cost.

The *read scale-out* feature is also available in the Hyperscale service tier when at least one [secondary replica](service-tier-hyperscale-replicas.md) is added. Hyperscale secondary [named replicas](service-tier-hyperscale-replicas.md#named-replica) provide independent scaling, access isolation, workload isolation, support for various read scale-out scenarios, and other benefits. Multiple secondary [HA replicas](service-tier-hyperscale-replicas.md#high-availability-replica) can be used for load-balancing read-only workloads that require more resources than available on one secondary HA replica.

The High Availability architecture of Basic, Standard, and General Purpose service tiers doesn't include any replicas. The *read scale-out* feature isn't available in these service tiers. However, when using Azure SQL Database, [geo-replicas](active-geo-replication-overview.md) can provide similar functionality in these service tiers.  When using Azure SQL Managed Instance and failover groups, the [failover group read-only listener](../managed-instance/auto-failover-group-sql-mi.md) can provide similar functionality respectively.

The following diagram illustrates the feature for Premium and Business Critical databases and managed instances.

:::image type="content" source="./media/read-scale-out/business-critical-service-tier-read-scale-out.png" alt-text="Diagram showing readonly replicas.":::

The *read scale-out* feature is enabled by default on new Premium,  Business Critical, and Hyperscale databases.

> [!NOTE]  
> Read scale-out is always enabled in the Business Critical service tier of SQL Managed Instance, and for Hyperscale databases with at least one secondary replica.

If your SQL connection string is configured with `ApplicationIntent=ReadOnly`, the application is redirected to a read-only replica of that database or managed instance. For information on how to use the `ApplicationIntent` property, see [Specifying Application Intent](/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery#specifying-application-intent).

For Azure SQL Database only, if you wish to ensure that the application connects to the primary replica regardless of the `ApplicationIntent` setting in the SQL connection string, you must explicitly disable read scale-out when creating the database or when altering its configuration. For example, if you upgrade your database from Standard or General Purpose tier to Premium or Business Critical and want to make sure all your connections continue to go to the primary replica, disable read scale-out. For details on how to disable it, see [Enable and disable read scale-out](#enable-and-disable-read-scale-out-for-sql-database).

> [!NOTE]  
> Query Store and SQL Profiler features are not supported on read-only replicas.

## Data consistency

Data changes made on the primary replica are persisted on read-only replicas synchronously or asynchronously depending on replica type. However, for all replica types, reads from a read-only replica are always asynchronous with respect to the primary. Within a session connected to a read-only replica, reads are always transactionally consistent. Because data propagation latency is variable, different replicas can return data at slightly different points in time relative to the primary and each other. If a read-only replica becomes unavailable and a session reconnects, it may connect to a replica that is at a different point in time than the original replica. Likewise, if an application changes data using a read-write session on the primary and immediately reads it using a read-only session on a read-only replica, it is possible that the latest changes aren't immediately visible.

Typical data propagation latency between the primary replica and read-only replicas varies in the range from tens of milliseconds to single-digit seconds. However, there is no fixed upper bound on data propagation latency. Conditions such as high resource utilization on the replica can increase latency substantially. Applications that require guaranteed data consistency across sessions, or require committed data to be readable immediately should use the primary replica.

> [!NOTE]  
> Data propagation latency includes the time required to send and persist (if applicable) log records to a secondary replica. It also includes the time required to redo (apply) these log records to data pages. To ensure data consistency, changes are not visible until the transaction commit log record is applied. When the workload uses larger transactions, effective data propagation latency is increased.
> 
> To monitor data propagation latency, see [Monitor and troubleshoot read-only replica](#monitor-and-troubleshoot-read-only-replicas).

## Connect to a read-only replica

When you enable read scale-out for a database, the `ApplicationIntent` option in the connection string provided by the client dictates whether the connection is routed to the write replica or to a read-only replica. Specifically, if the `ApplicationIntent` value is `ReadWrite` (the default value), the connection is directed to the read-write replica. This is identical to the behavior when `ApplicationIntent` isn't included in the connection string. If the `ApplicationIntent` value is `ReadOnly`, the connection is routed to a read-only replica.

For example, the following connection string connects the client to a read-only replica (replacing the items in the angle brackets with the correct values for your environment and dropping the angle brackets):

```sql
Server=tcp:<server>.database.windows.net;Database=<mydatabase>;ApplicationIntent=ReadOnly;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;
```

To connect to a read-only replica using SQL Server Management Studio (SSMS), select **Options**

:::image type="content" source="media/read-scale-out/ssms-options-screen.png" alt-text="Screenshot showing the SSMS Options button.":::

Select **Additional Connection Parameters** and enter `ApplicationIntent=ReadOnly` and then select **Connect**

:::image type="content" source="media/read-scale-out/ssms-additional-connection-parameters-screen.png" alt-text="Screenshot showing SSMS Additional Connection Parameters.":::

Either of the following connection strings connects the client to a read-write replica (replacing the items in the angle brackets with the correct values for your environment and dropping the angle brackets):

```text
Server=tcp:<server>.database.windows.net;Database=<mydatabase>;ApplicationIntent=ReadWrite;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;

Server=tcp:<server>.database.windows.net;Database=<mydatabase>;User ID=<myLogin>;Password=<myPassword>;Trusted_Connection=False; Encrypt=True;
```

## Verify that a connection is to a read-only replica

You can verify whether you are connected to a read-only replica by running the following query in the context of your database. It returns READ_ONLY when you are connected to a read-only replica.

```sql
SELECT DATABASEPROPERTYEX(DB_NAME(), 'Updateability');
```

> [!NOTE]  
> In Premium and Business Critical service tiers, only one of the read-only replicas is accessible at any given time. Hyperscale supports multiple read-only replicas.

## Monitor and troubleshoot read-only replicas

When connected to a read-only replica, Dynamic Management Views (DMVs) reflect the state of the replica, and can be queried for monitoring and troubleshooting purposes. The database engine provides multiple views to expose a wide variety of monitoring data.

The following views are commonly used for replica monitoring and troubleshooting:

| Name | Purpose |
| :--- | :--- |
| [sys.dm_db_resource_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database) | Provides resource utilization metrics for the last hour, including CPU, data IO, and log write utilization relative to service objective limits. |
| [sys.dm_os_wait_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) | Provides aggregate wait statistics for the database engine instance. |
| [sys.dm_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-replica-states-azure-sql-database) | Provides replica health state and synchronization statistics. Redo queue size and redo rate serve as indicators of data propagation latency on the read-only replica. |
| [sys.dm_os_performance_counters](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql) | Provides database engine performance counters. |
| [sys.dm_exec_query_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) | Provides per-query execution statistics such as number of executions, CPU time used, etc. |
| [sys.dm_exec_query_plan()](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql) | Provides cached query plans. |
| [sys.dm_exec_sql_text()](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql) | Provides query text for a cached query plan. |
| [sys.dm_exec_query_profiles](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql) | Provides real time query progress while queries are in execution. |
| [sys.dm_exec_query_plan_stats()](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql) | Provides the last known actual execution plan including runtime statistics for a query. |
| [sys.dm_io_virtual_file_stats()](/sql/relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql) | Provides storage IOPS, throughput, and latency statistics for all database files. |

> [!NOTE]  
> The `sys.resource_stats` and `sys.elastic_pool_resource_stats` DMVs in the logical `master` database return resource utilization data of the primary replica.

### Monitor read-only replicas with Extended Events

An extended event session can't be created when connected to a read-only replica. However, in Azure SQL Database, the definitions of database-scoped [Extended Event](xevent-db-diff-from-svr.md) sessions created and altered on the primary replica replicate to read-only replicas, including geo-replicas, and capture events on read-only replicas.

An extended event session on a read-only replica that is based on a session definition from the primary replica can be started and stopped independently of the primary replica. When an extended event session is dropped on the primary replica, it is also dropped on all read-only replicas.

### Transaction isolation level on read-only replicas

Transactions on read-only replicas always use the snapshot [transaction isolation level](/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide#database-engine-isolation-levels), regardless of transaction isolation level of the session, and regardless of any query hints. Snapshot isolation uses row versioning to avoid blocking scenarios where readers block writers.

In rare cases, if a snapshot isolation transaction accesses object metadata that has been modified in another concurrent transaction, it may receive error [3961](/sql/relational-databases/errors-events/mssqlserver-3961-database-engine-error), "Snapshot isolation transaction failed in database '%.*ls' because the object accessed by the statement has been modified by a DDL statement in another concurrent transaction since the start of this transaction. It is disallowed because the metadata is not versioned. A concurrent update to metadata can lead to inconsistency if mixed with snapshot isolation."

### Long-running queries on read-only replicas

Queries running on read-only replicas need to access metadata for the objects referenced in the query (tables, indexes, statistics, etc.) In rare cases, if object metadata is modified on the primary replica while a query holds a lock on the same object on the read-only replica, the query can [block](/sql/database-engine/availability-groups/windows/troubleshoot-primary-changes-not-reflected-on-secondary#BKMK_REDOBLOCK) the process that applies changes from the primary replica to the read-only replica. If such a query were to run for a long time, it would cause the read-only replica to be significantly out of sync with the primary replica. For replicas that are potential failover targets (secondary replicas in Premium and Business Critical service tiers, Hyperscale HA replicas, and all geo-replicas), this would also delay database recovery if a failover were to occur, causing longer than expected downtime.

If a long-running query on a read-only replica directly or indirectly causes this kind of blocking, it may be automatically terminated to avoid excessive data latency and potential database availability impact. The session receives error 1219, "Your session has been disconnected because of a high priority DDL operation", or error 3947, "The transaction was aborted because the secondary compute failed to catch up redo. Retry the transaction."

> [!NOTE]  
> If you receive error 3961, 1219, or 3947 when running queries against a read-only replica, retry the query. Alternatively, avoid operations that modify object metadata (schema changes, index maintenance, statistics updates, etc.) on the primary replica while long-running queries execute on secondary replicas.

> [!TIP]  
> In Premium and Business Critical service tiers, when connected to a read-only replica, the `redo_queue_size` and `redo_rate` columns in the [sys.dm_database_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-replica-states-azure-sql-database) DMV may be used to monitor data synchronization process, serving as indicators of data propagation latency on the read-only replica.
>

## Enable and disable read scale-out for SQL Database

For SQL Managed Instance, read-scale out is automatically enabled on the Business Critical service tier, and isn't available in the General Purpose service tier.  Disabling and reenabling read scale-out isn't possible.

For SQL Database, read scale-out is enabled by default on Premium, Business Critical, and Hyperscale service tiers. Read scale-out can't be enabled in Basic, Standard, or General Purpose service tiers. Read scale-out is automatically disabled on Hyperscale databases configured with zero secondary replicas.

For single and pooled databases in Azure SQL Database, you can disable and re-enable read scale-out in the Premium or Business Critical service tiers by using the Azure portal, and Azure PowerShell. These options aren't available for SQL Managed Instance as read-scale out can't be disabled.

> [!NOTE]  
> For single databases and elastic pool databases, the ability to disable read scale-out is provided for backward compatibility. Read scale-out cannot be disabled on Business Critical managed instances.

### Azure portal

For Azure SQL Database, you can manage the read scale-out setting on the **Compute + storage** database pane, available under **Settings**. Using the Azure portal to enable or disable read scale-out isn't available for Azure SQL Managed Instance.

### PowerShell

> [!IMPORTANT]  
> The PowerShell Azure Resource Manager module is still supported, but all future development is for the Az.Sql module. The Azure Resource Manager module will continue to receive bug fixes until at least December 2020.  The arguments for the commands in the Az module and in the Azure Resource Manager modules are substantially identical. For more information about their compatibility, see [Introducing the new Azure PowerShell Az module](/powershell/azure/new-azureps-module-az).

Managing read scale-out in Azure PowerShell requires the December 2016 Azure PowerShell release or newer. For the newest PowerShell release, see [Azure PowerShell](/powershell/azure/install-az-ps).

In Azure SQL Database, you can disable or re-enable read scale-out in Azure PowerShell by invoking the [Set-AzSqlDatabase](/powershell/module/az.sql/set-azsqldatabase) cmdlet and passing in the desired value  (`Enabled` or `Disabled`) for the `-ReadScale` parameter. Disabling read scale-out for SQL Managed Instance isn't available.

To disable read scale-out on an existing database (replacing the items in the angle brackets with the correct values for your environment and dropping the angle brackets):

```powershell
Set-AzSqlDatabase -ResourceGroupName <resourceGroupName> -ServerName <serverName> -DatabaseName <databaseName> -ReadScale Disabled
```

To disable read scale-out on a new database (replacing the items in the angle brackets with the correct values for your environment and dropping the angle brackets):

```powershell
New-AzSqlDatabase -ResourceGroupName <resourceGroupName> -ServerName <serverName> -DatabaseName <databaseName> -ReadScale Disabled -Edition Premium
```

To re-enable read scale-out on an existing database (replacing the items in the angle brackets with the correct values for your environment and dropping the angle brackets):

```powershell
Set-AzSqlDatabase -ResourceGroupName <resourceGroupName> -ServerName <serverName> -DatabaseName <databaseName> -ReadScale Enabled
```

### REST API

To create a database with read scale-out disabled, or to change the setting for an existing database, use the following method with the `readScale` property set to `Enabled` or `Disabled`, as in the following sample request.

```rest
Method: PUT
URL: https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{GroupName}/providers/Microsoft.Sql/servers/{ServerName}/databases/{DatabaseName}?api-version= 2014-04-01-preview
Body: {
   "properties": {
      "readScale":"Disabled"
   }
}
```

For more information, see [Databases - Create or update](/rest/api/sql/2022-08-01-preview/databases/create-or-update).

## Use the `tempdb` database on a read-only replica

The `tempdb` database on the primary replica isn't replicated to the read-only replicas. Each replica has its own `tempdb` database that is created when the replica is created. This ensures that `tempdb` is updateable and can be modified during your query execution. If your read-only workload depends on using `tempdb` objects, you should create these objects as part of the same workload, while connected to a read-only replica.

## Use read scale-out with geo-replicated databases

Geo-replicated secondary databases have the same High Availability architecture as primary databases. If you're connecting to the geo-replicated secondary database with read scale-out enabled, your sessions with `ApplicationIntent=ReadOnly` are routed to one of the high availability replicas in the same way they are routed on the primary writeable database. The sessions without `ApplicationIntent=ReadOnly` are routed to the primary replica of the geo-replicated secondary, which is also read-only.

In this fashion, creating a geo-replica can provide multiple additional read-only replicas for a read-write primary database. Each additional geo-replica provides another set of read-only replicas. Geo-replicas can be created in any Azure region, including the region of the primary database.

> [!NOTE]  
> There is no automatic round-robin or any other load-balanced routing between the replicas of a geo-replicated secondary database, with the exception of a Hyperscale geo-replica with more than one HA replica. In that case, sessions with read-only intent are distributed over all HA replicas of a geo-replica.

## Feature support on read-only replicas

A list of the behavior of some features on read-only replicas follows:

- Auditing on read-only replicas is automatically enabled. For more information about the hierarchy of the storage folders, naming conventions, and log format, see [SQL Database Audit Log Format](audit-log-format.md).
- [Query Performance Insight](query-performance-insight-use.md) relies on data from the [Query Store](/sql/relational-databases/performance/monitoring-performance-by-using-the-query-store), which currently doesn't track activity on the read-only replica. Query Performance Insight doesn't show queries that execute on the read-only replica.
- Automatic tuning relies on the Query Store, as detailed in the [Automatic tuning paper](https://www.microsoft.com/research/uploads/prod/2019/02/autoindexing_azuredb.pdf). Automatic tuning only works for workloads running on the primary replica.

## Next steps

- For information about SQL Database Hyperscale offering, see [Hyperscale service tier](service-tier-hyperscale.md).
