---
title: "sys.dm_hadr_database_replica_cluster_states (Transact-SQL)"
description: sys.dm_hadr_database_replica_cluster_states displays health information for availability databases in an AG on Windows Server failover clusters.
author: rwestMSFT
ms.author: randolphwest
ms.date: 04/17/2023
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_hadr_database_replica_cluster_states"
  - "dm_hadr_database_replica_cluster_states_TSQL"
  - "sys.dm_hadr_database_replica_cluster_states_TSQL"
  - "dm_hadr_database_replica_cluster_states"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "Availability Groups [SQL Server], WSFC clusters"
  - "sys.dm_hadr_database_replica_cluster_states dynamic management view"
dev_langs:
  - "TSQL"
---
# sys.dm_hadr_database_replica_cluster_states (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Returns a row containing insight into the health of the availability databases in the Always On availability groups in each Always On availability group on the Windows Server Failover Clustering (WSFC) cluster. Query `sys.dm_hadr_database_replica_cluster_states` to answer the following questions:

- Are all databases in an availability group ready for a failover?

- After a forced failover, has a secondary database suspended itself locally and acknowledged its suspended state to the new primary replica?

- If the primary replica is currently unavailable, which secondary replica would allow the minimum data loss if it becomes the primary replica?

- When the value of the [sys.databases](../system-catalog-views/sys-databases-transact-sql.md) `log_reuse_wait_desc` column is `AVAILABILITY_REPLICA`, which secondary replica in an availability group is holding up log truncation on a given primary database?

| Column name | Data type | Description |
| --- | --- | --- |
| **replica_id** | **uniqueidentifier** | Identifier of the availability replica within the availability group. |
| **group_database_id** | **uniqueidentifier** | Identifier of the database within the availability group. This identifier is identical on every replica to which this database is joined. |
| **database_name** | **sysname** | Name of a database that belongs to the availability group. |
| **is_failover_ready** | **bit** | Indicates whether the secondary database is synchronized with the corresponding primary database. one of:<br /><br />0 = The database isn't marked as synchronized in the cluster. The database isn't ready for a failover.<br /><br />1 = The database is marked as synchronized in the cluster. The database is ready for a failover. |
| **is_pending_secondary_suspend** | **bit** | Indicates whether, after a forced failover, the database is pending suspension, one of:<br /><br />0 = Any states except for HADR_SYNCHRONIZED_SUSPENDED.<br /><br />1 = HADR_SYNCHRONIZED_SUSPENDED. When a forced failover completes, each of the secondary databases is set to HADR_SYNCHONIZED_SUSPENDED and remains in this state until the new primary replica receives an acknowledgment from that secondary database to the SUSPEND message.<br /><br />NULL = Unknown (no quorum) |
| **is_database_joined** | **bit** | Indicates whether the database on this availability replica has been joined to the availability group, one of:<br /><br />0 = Database isn't joined to the availability group on this availability replica.<br /><br />1 = Database is joined to the availability group on this availability replica.<br /><br />NULL = unknown (The availability replica lacks quorum.) |
| **recovery_lsn** | **numeric(25,0)** | On the primary replica, the end of the transaction log before the replica writes any new log records after recovery or failover. On the primary replica, the row for a given secondary database has the value that the primary replica needs the secondary replica to synchronize to (that is, to revert to and reinitialize to).<br /><br />On secondary replicas, this value is NULL. Each secondary replica has either the MAX value or a lower value that the primary replica has told the secondary replica to go back to. |
| **truncation_lsn** | **numeric(25,0)** | The [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] log truncation value, which may be higher than the local truncation LSN if local log truncation is blocked (such as by a backup operation). |

## Permissions

For [!INCLUDE [sssql19-md](../../includes/sssql19-md.md)] and earlier versions, requires VIEW SERVER STATE permission on the server.

For [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later versions, requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also

- [Always On Availability Groups Dynamic Management Views and Functions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)
- [Always On Availability Groups Catalog Views (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)
- [Monitor Availability Groups (Transact-SQL)](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)
- [Always On Availability Groups (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)
- [sys.dm_hadr_database_replica_states (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)
