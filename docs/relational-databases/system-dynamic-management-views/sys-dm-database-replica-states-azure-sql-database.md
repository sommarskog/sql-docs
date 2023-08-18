---
title: "sys.dm_database_replica_states (Azure SQL Database)"
description: sys.dm_database_replica_states returns state information for each database that participates in primary and secondary replicas.
author: rwestMSFT
ms.author: randolphwest
ms.date: 06/19/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_database_replica_states_TSQL"
  - "sys.dm_database_replica_states"
  - "dm_database_replica_states"
  - "dm_database_replica_states_TSQL"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "sys.dm_database_replica_states dynamic management view"
dev_langs:
  - "TSQL"
---
# sys.dm_database_replica_states (Azure SQL Database)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Returns state information for each database that participates in primary and secondary replicas. On a secondary replica, returns one row for every secondary database on the instance. On the primary replica, returns one row for the primary database, and an additional row for each secondary database.

> [!IMPORTANT]  
> Depending on the action and higher-level states, database-state information may be unavailable or out of date. Furthermore, the values have only local relevance.

| Column name | Data type | Description (on primary replica) |
| --- | --- | --- |
| **database_id** | **int** | Identifier of the database. <br /><br />In [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], the values are unique within a single database or an elastic pool, but not within a logical server.|
| **group_id** | **uniqueidentifier** | Identifier of the availability group to which the database belongs. |
| **replica_id** | **uniqueidentifier** | Identifier of the availability replica within the availability group. |
| **group_database_id** | **uniqueidentifier** | Identifier of the database within the availability group. This identifier is identical on every replica to which this database is joined. |
| **is_local** | **bit** | Whether the availability database is local, one of:<br /><br />0 = The database isn't local to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.<br /><br />1 = The database is local to the server instance. |
| **is_primary_replica** | **bit** | Returns 1 if the replica is primary, or 0 if it is a secondary replica in the availability group to which the database belongs. This doesn't refer to the primary or secondary database in a distributed availability group or an active geo-replication relation.<br /><br />**Applies to:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] and later versions. |
| **synchronization_state** | **tinyint** | Data-movement state, one of the following values.<br /><br />0 = Not synchronizing. For a primary database, indicates that the database isn't ready to synchronize its transaction log with the corresponding secondary databases. For a secondary database, indicates that the database hasn't started log synchronization because of a connection issue, is being suspended, or is going through transition states during startup or a role switch.<br /><br />1 = Synchronizing. For a primary database, indicates that the database is ready to accept a scan request from a secondary database. For a secondary database, indicates that active data movement is occurring for the database.<br /><br />2 = Synchronized. A primary database shows SYNCHRONIZED in place of SYNCHRONIZING. A synchronous-commit secondary database shows synchronized when the local cache says the database is failover ready and is synchronizing.<br /><br />3 = Reverting. Indicates the phase in the undo process when a secondary database is actively getting pages from the primary database.<br /><br />**Important:** When a database on a secondary replica is in the REVERTING state, forcing failover to the secondary replica leaves the database in a state in which it can't be started as a primary database. Either the database needs to reconnect as a secondary database, or you need to apply new log records from a log backup.<br /><br />4 = Initializing. Indicates the phase of undo when the transaction log required for a secondary database to catch up to the undo LSN is being shipped and hardened on a secondary replica.<br /><br />**Important:** When a database on a secondary replica is in the INITIALIZING state, forcing failover to the secondary replica leaves the database in a state in which it can't be started as a primary database. Either the database needs to reconnect as a secondary database, or you need to apply new log records from a log backup. |
| **synchronization_state_desc** | **nvarchar(60)** | Description of the data-movement state, one of:<br /><br />- NOT SYNCHRONIZING<br />- SYNCHRONIZING<br />- SYNCHRONIZED<br />- REVERTING<br />- INITIALIZING |
| **is_commit_participant** | **bit** | 0 = Transaction commit isn't synchronized with respect to this database.<br /><br />1 = Transaction commit is synchronized with respect to this database.<br /><br />For a database on an asynchronous-commit availability replica, this value is always 0.<br /><br />For a database on a synchronous-commit availability replica, this value is accurate only on the primary database. |
| **synchronization_health** | **tinyint** | Reflects the intersection of the synchronization state of a database that is joined to the availability group on the availability replica and the availability mode of the availability replica (synchronous-commit or asynchronous-commit mode), one of the following values.<br /><br />0 = Not healthy. The `synchronization_state` of the database is 0 (NOT SYNCHRONIZING).<br /><br />1 = Partially healthy. A database on a synchronous-commit availability replica is considered partially healthy if `synchronization_state` is 1 (SYNCHRONIZING).<br /><br />2 = Healthy. A database on a synchronous-commit availability replica is considered healthy if `synchronization_state` is 2 (SYNCHRONIZED), and a database on an asynchronous-commit availability replica is considered healthy if `synchronization_state` is 1 (SYNCHRONIZING). |
| **synchronization_health_desc** | **nvarchar(60)** | Description of the `synchronization_health` of the availability database.<br /><br />- NOT_HEALTHY<br />- PARTIALLY_HEALTHY<br />- HEALTHY |
| **database_state** | **tinyint** | 0 = Online<br />1 = Restoring<br />2 = Recovering<br />3 = Recovery pending<br />4 = Suspect<br />5 = Emergency<br />6 = Offline<br /><br />**Note:** Same as the `state` column in `sys.databases`. |
| **database_state_desc** | **nvarchar(60)** | Description of the `database_state` of the availability replica.<br /><br />- ONLINE<br />- RESTORING<br />- RECOVERING<br />- RECOVERY_PENDING<br />- SUSPECT<br />- EMERGENCY<br />- OFFLINE<br /><br />**Note:** Same as the `state_desc` column in `sys.databases`. |
| **is_suspended** | **bit** | Database state, one of:<br /><br />0 = Resumed<br />1 = Suspended |
| **suspend_reason** | **tinyint** | If the database is suspended, the reason for the suspended state, one of:<br /><br />0 = User action<br />1 = Suspend from partner<br />2 = Redo<br />3 = Capture<br />4 = Apply<br />5 = Restart<br />6 = Undo<br />7 = Revalidation<br />8 = Error in the calculation of the secondary-replica synchronization point |
| **suspend_reason_desc** | **nvarchar(60)** | Description of the database suspended state reason, one of:<br /><br />SUSPEND_FROM_USER = A user manually suspended data movement<br /><br />SUSPEND_FROM_PARTNER = The database replica is suspended after a forced failover<br /><br />SUSPEND_FROM_REDO = An error occurred during the redo phase<br /><br />SUSPEND_FROM_APPLY = An error occurred when writing the log to file (see error log)<br /><br />SUSPEND_FROM_CAPTURE = An error occurred while capturing log on the primary replica<br /><br />SUSPEND_FROM_RESTART = The database replica was suspended before the database was restarted (see error log)<br /><br />SUSPEND_FROM_UNDO = An error occurred during the undo phase (see error log)<br /><br />SUSPEND_FROM_REVALIDATION = Log change mismatch is detected on reconnection (see error log)<br /><br />SUSPEND_FROM_XRF_UPDATE = Unable to find the common log point (see error log) |
| **recovery_lsn** | **numeric(25,0)** | On the primary replica, the end of the transaction log before the primary database writes any new log records after recovery or failover. For a given secondary database, if this value is less than the current hardened LSN (`last_hardened_lsn`), `recovery_lsn` is the value to which this secondary database would need to resynchronize (that is, to revert to and reinitialize to). If this value is greater than or equal to the current hardened LSN, resynchronization would be unnecessary and wouldn't occur.<br /><br />`recovery_lsn` reflects a log-block ID padded with zeroes. It isn't an actual log sequence number (LSN). |
| **truncation_lsn** | **numeric(25,0)** | On the primary replica, for the primary database, reflects the minimum log truncation LSN across all the corresponding secondary databases. If local log truncation is blocked (such as by a backup operation), this LSN might be higher than the local truncation LSN.<br /><br />For a given secondary database, reflects the truncation point of that database.<br /><br />**truncation_lsn** reflects a log-block ID padded with zeroes. It isn't an actual log sequence number. |
| **last_sent_lsn** | **numeric(25,0)** | The log block identifier that indicates the point up to which all log blocks have been sent by the primary. This is the ID of the next log block that will be sent, rather than the ID of the most recently sent log block.<br /><br />`last_sent_lsn` reflects a log-block ID padded with zeroes. It isn't an actual log sequence number. |
| **last_sent_time** | **datetime** | Time when the last log block was sent. |
| **last_received_lsn** | **numeric(25,0)** | Log block ID identifying the point up to which all log blocks have been received by the secondary replica that hosts this secondary database.<br /><br />`last_received_lsn` reflects a log-block ID padded with zeroes. It isn't an actual log sequence number. |
| **last_received_time** | **datetime** | Time when the log block ID in last message received was read on the secondary replica. |
| **last_hardened_lsn** | **numeric(25,0)** | Start of the Log Block containing the log records of last hardened LSN on a secondary database.<br /><br />On an asynchronous-commit primary database or on a synchronous-commit database whose current policy is "delay", the value is NULL. For other synchronous-commit primary databases, `last_hardened_lsn` indicates the minimum of the hardened LSN across all the secondary databases.<br /><br />**Note:** `last_hardened_lsn` reflects a log-block ID padded with zeroes. It isn't an actual log sequence number. |
| **last_hardened_time** | **datetime** | On a secondary database, time of the log-block identifier for the last hardened LSN (`last_hardened_lsn`). On a primary database, reflects the time corresponding to minimum hardened LSN. |
| **last_redone_lsn** | **numeric(25,0)** | Actual log sequence number of the last log record that was redone on the secondary database. `last_redone_lsn` is always less than `last_hardened_lsn`. |
| **last_redone_time** | **datetime** | Time when the last log record was redone on the secondary database. |
| **log_send_queue_size** | **bigint** | The amount of log records of the primary database that hasn't been sent to the secondary databases, in kilobytes (KB). |
| **log_send_rate** | **bigint** | Average rate at which primary replica instance sent data during last active period, in kilobytes (KB)/second. |
| **redo_queue_size** | **bigint** | The amount of log records in the log files of the secondary replica that hasn't yet been redone, in kilobytes (KB). |
| **redo_rate** | **bigint** | Average rate at which the log records are being redone on a given secondary database, in kilobytes (KB)/second.<br /><br />`redo_rate` is calculated by dividing the total log bytes redone since database engine startup by the time span when redo was actively running, rather than by the elapsed time. Because redo may not be running continuously, resulting value may be different (higher) than the value of `Database Replica:Redone Bytes/sec` performance counter. |
| **filestream_send_rate** | **bigint** | The rate at which the FILESTREAM files are shipped to the secondary replica, in kilobytes (KB)/second. |
| **end_of_log_lsn** | **numeric(25,0)** | Local end of log LSN. Actual LSN corresponding to the last log record in the log cache on the primary and secondary databases. On the primary replica, the secondary rows reflect the end of log LSN from the latest progress messages that the secondary replicas have sent to the primary replica.<br /><br />`end_of_log_lsn` reflects a log-block ID padded with zeroes. It isn't an actual log sequence number. |
| **last_commit_lsn** | **numeric(25,0)** | Actual log sequence number corresponding to the last commit record in the transaction log.<br /><br />On the primary database, this corresponds to the last commit record processed. Rows for secondary databases show the log sequence number that the secondary replica has sent to the primary replica.<br /><br />On the secondary replica, this is the last commit record that was redone. |
| **last_commit_time** | **datetime** | Time corresponding to the last commit record.<br /><br />On the secondary database, this time is the same as on the primary database.<br /><br />On the primary replica, each secondary database row displays the time that the secondary replica that hosts that secondary database has reported back to the primary replica. The difference in time between the primary-database row and a given secondary-database row represents approximately the recovery point objective (RPO), assuming that the redo process is caught up and that the progress has been reported back to the primary replica by the secondary replica. |
| **low_water_mark_for_ghosts** | **bigint** | A monotonically increasing number for the database indicating a low water mark used by ghost cleanup on the primary database. If this number isn't increasing over time, it implies that ghost cleanup might not happen. To decide which ghost rows to clean up, the primary replica uses the minimum value of this column for this database across all availability replicas (including the primary replica). |
| **secondary_lag_seconds** | **bigint** | The number of seconds that the secondary replica is behind the primary replica during synchronization.<br /><br />**Applies to:** [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] and later versions. |
| **quorum_commit_lsn** | **numeric(25,0)** | Identified for informational purposes only. Not supported. Future compatibility isn't guaranteed. |
| **quorum_commit_time** | **datetime** | Identified for informational purposes only. Not supported. Future compatibility isn't guaranteed. |

## Permissions

Requires VIEW DATABASE STATE permission on the database.

## See also

- [Always On Availability Groups (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)
- [Monitor Availability Groups (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)
