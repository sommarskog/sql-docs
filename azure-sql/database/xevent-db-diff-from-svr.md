---
title: Extended events
description: Describes extended events (XEvents) in Azure SQL Database, and how event sessions differ slightly from event sessions in Microsoft SQL Server.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: wiassaf, mathoma
ms.date: 01/30/2023
ms.service: sql-database
ms.subservice: performance
ms.topic: reference
ms.custom: sqldbrb=1
monikerRange: "= azuresql || = azuresql-db || = azuresql-mi"
---
# Extended events in Azure SQL Database 
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

[!INCLUDE [sql-database-xevents-selectors-1-include](../includes/sql-database-xevents-selectors-1-include.md)]

The feature set of extended events in Azure SQL Database is a robust subset of the features on SQL Server and Azure SQL Managed Instance.

*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.

Additional information about extended events is available at:

- [Quick Start: Extended events in SQL Server](/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
- [Extended Events](/sql/relational-databases/extended-events/extended-events)

## Prerequisites

This article assumes you already have some knowledge of:

- [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)
- [Extended events](/sql/relational-databases/extended-events/extended-events)

- The bulk of our documentation about extended events applies to SQL Server, Azure SQL Database, and Azure SQL Managed Instance.

Prior exposure to the following items is helpful when choosing the Event File as the [target](#AzureXEventsTargets):

- [Azure Storage service](https://azure.microsoft.com/services/storage/)

- [Azure PowerShell with Azure Storage](/powershell/module/az.storage/)

## Code samples

Related articles provide two code samples:

- [Ring Buffer target code for extended events in Azure SQL Database](xevent-code-ring-buffer.md)

  - Short simple Transact-SQL script.
  - We emphasize in the code sample article that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement. Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.

- [Event File target code for extended events in Azure SQL Database](xevent-code-event-file.md)

  - Phase 1 is PowerShell to create an Azure Storage container.
  - Phase 2 is Transact-SQL that uses the Azure Storage container.

## Transact-SQL differences

- When you execute the [CREATE EVENT SESSION](/sql/t-sql/statements/create-event-session-transact-sql) command on SQL Server, you use the **ON SERVER** clause. But on Azure SQL Database you use the **ON DATABASE** clause instead.
- The **ON DATABASE** clause also applies to the [ALTER EVENT SESSION](/sql/t-sql/statements/alter-event-session-transact-sql) and [DROP EVENT SESSION](/sql/t-sql/statements/drop-event-session-transact-sql) Transact-SQL commands.

- A best practice is to include the event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.
  - The **= ON** value supports an automatic restart after a reconfiguration of the logical database due to a failover.

## New catalog views

The extended events feature is supported by several [catalog views](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql). Catalog views tell you about *metadata or definitions* of user-created event sessions in the current database. The views do not return information about instances of active event sessions.

| Name of catalog view | Description |
|:--- |:--- |
| [sys.database_event_session_actions](/sql/relational-databases/system-catalog-views/sys-database-event-session-actions-azure-sql-database) |Returns a row for each action on each event of an event session. |
| [sys.database_event_session_events](/sql/relational-databases/system-catalog-views/sys-database-event-session-events-azure-sql-database) |Returns a row for each event in an event session. |
| [sys.database_event_session_fields](/sql/relational-databases/system-catalog-views/sys-database-event-session-fields-azure-sql-database) |Returns a row for each customize-able column that was explicitly set on events and targets. |
| [sys.database_event_session_targets](/sql/relational-databases/system-catalog-views/sys-database-event-session-targets-azure-sql-database) |Returns a row for each event target for an event session. |
| [sys.database_event_sessions](/sql/relational-databases/system-catalog-views/sys-database-event-sessions-azure-sql-database) |Returns a row for each event session in the database. |

In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*. The name pattern is like `sys.server_event_%`.

## New dynamic management views [(DMVs)](/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views)

Azure SQL Database has [dynamic management views (DMVs)](/sql/relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views) that support extended events. DMVs tell you about *active* event sessions.

| Name of DMV | Description |
|:--- |:--- |
| [sys.dm_xe_database_session_event_actions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-database-session-event-actions-azure-sql-database) |Returns information about event session actions. |
| [sys.dm_xe_database_session_events](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-database-session-events-azure-sql-database) |Returns information about session events. |
| [sys.dm_xe_database_session_object_columns](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-database-session-object-columns-azure-sql-database) |Shows the configuration values for objects that are bound to a session. |
| [sys.dm_xe_database_session_targets](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-database-session-targets-azure-sql-database) |Returns information about session targets. |
| [sys.dm_xe_database_sessions](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-database-sessions-azure-sql-database) |Returns a row for each event session that is scoped to the current database. |

In Microsoft SQL Server, similar catalog views are named without the *\_database* portion of the name, such as:

- `sys.dm_xe_sessions` instead of `sys.dm_xe_database_sessions`.

### DMVs common to both

For extended events there are additional DMVs that are common to Azure SQL Database, Azure SQL Managed Instance, and Microsoft SQL Server:

- [sys.dm_xe_map_values](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql)
- [sys.dm_xe_object_columns](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql)
- [sys.dm_xe_objects](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)
- [sys.dm_xe_packages](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)

<a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## Find the available extended events, actions, and targets

To obtain a list of the available events, actions, and target, use the sample query:

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```

<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## Targets for your Azure SQL Database event sessions

Here are targets that can capture results from your event sessions on Azure SQL Database:

- [Ring Buffer target](/sql/relational-databases/extended-events/targets-for-extended-events-in-sql-server#ring_buffer-target) - Briefly holds event data in memory.
- [Event Counter target](/sql/relational-databases/extended-events/targets-for-extended-events-in-sql-server#event_counter-target) - Counts all events that occur during an extended events session.
- [Event File target](/sql/relational-databases/extended-events/targets-for-extended-events-in-sql-server#event_file-target) - Writes complete buffers to an Azure Storage container.

The [Event Tracing for Windows (ETW)](/dotnet/framework/wcf/samples/etw-tracing) API is not available for extended events on Azure SQL Database.

## Restrictions

There are a couple of security-related differences befitting the cloud environment of Azure SQL Database:

- Extended events are founded on the single-tenant isolation model. An event session in one database cannot access data or events from another database.
- You cannot issue a `CREATE EVENT SESSION` statement in the context of the `master` database.
    
## Permission model

You must have **Control** permission on the database to issue a `CREATE EVENT SESSION` statement. The database owner (dbo) has **Control** permission.

### Storage container authorizations

The SAS token you generate for your Azure Storage container must specify **rwl** for the permissions. The **rwl** value provides the following permissions:

- Read
- Write
- List

## Performance considerations

There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for the overall system. Therefore Azure SQL Database dynamically sets and adjusts limits on the amount of active memory that can be accumulated by an event session. Many factors go into the dynamic calculation.

There is a cap on memory available to XEvent sessions in Azure SQL Database:
  - In single Azure SQL Database in the DTU purchasing model, each database can use up to 128 MB. This is raised to 256 MB only in the Premium tier.
  - In single Azure SQL Database in the vCore purchasing model, each database can use up to 128 MB.
  - In an elastic pool, individual databases are limited by the single database limits, and in total they cannot exceed 512 MB.

If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:

- Run fewer concurrent event sessions.
- Through your **CREATE** and **ALTER** statements for event sessions, reduce the amount of memory you specify on the **MAX\_MEMORY** clause.

There is a cap on number of started XEvent sessions in Azure SQL Database:
  - In a single Azure SQL Database, the limit is 100.
  - In an elastic pool, the limit is 100 database-scoped sessions per pool.
 
In [dense elastic pools](elastic-pool-resource-management.md), starting a new extended event session may fail due to memory constraints even when the total number of started sessions is below 100.
  


### Network latency

The **Event File** target might experience network latency or failures while persisting data to Azure Storage blobs. Other events in Azure SQL Database might be delayed while they wait for the network communication to complete. This delay can slow your workload.

- To mitigate this performance risk, avoid setting the **EVENT_RETENTION_MODE** option to **NO_EVENT_LOSS** in your event session definitions.

## Related links

- [Azure Storage Cmdlets](/powershell/module/Azure.Storage)
- [Using Azure PowerShell with Azure Storage](/powershell/module/az.storage/)
- [How to use Blob storage from .NET](/azure/storage/blobs/storage-quickstart-blobs-dotnet)
- [CREATE CREDENTIAL (Transact-SQL)](/sql/t-sql/statements/create-credential-transact-sql)
- [CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)
- The Azure *Service Updates* webpage, narrowed by parameter to Azure SQL Database:
  - [https://azure.microsoft.com/updates/?service=sql-database](https://azure.microsoft.com/updates/?service=sql-database)

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](/sql/relational-databases/extended-events/determine-which-queries-are-holding-locks)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](/sql/relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them)
-->
