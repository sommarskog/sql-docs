---
title: "Create a database snapshot for an availability group"
description: "Describes how to create a database snapshot for a database within an Always On availability group on either the primary or secondary database."
author: MashaMSFT
ms.author: mathoma
ms.date: "05/17/2016"
ms.service: sql
ms.subservice: availability-groups
ms.topic: how-to
helpviewer_keywords:
  - "database snapshots [SQL Server], AlwaysOn Availability Groups"
  - "database snapshots [SQL Server], Always On Availability Groups"
  - "Availability Groups [SQL Server], interoperability"
---
# Database Snapshots with Always On Availability Groups (SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

[!NOTE] Creating database snapshots on any database has cpu and IO overhead due to copy on write activity. On database replicas, this can hurt redo throughput among other operations, especially as the number of snapshots increases.

  You can create a database snapshot on an primary or secondary database in an availability group. The replica role must be either PRIMARY or SECONDARY, not in the RESOLVING state.  
  
 We recommend that the database synchronization state be SYNCHRONIZING or SYNCHRONIZED when you create a database snapshot. However, database snapshots can be created when the database synchronization state is NOT SYNCHRONIZING.  
  
 A database snapshot on a secondary replica should continue to work if the replica is DISCONNECTED from the primary replica.  
  
 Some [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] conditions cause both the source database and its database snapshots to be restarted, temporarily disconnecting users. These conditions are as follows:  
  
-   The primary replica changes roles, whether because the current primary replica goes off line and comes back online on the same server instance or because the availability group fails over.  
  
-   The database enters the secondary role.  
  
 If the availability replica that hosts database snapshots is failed over, the database snapshots remain on the server instance where they were created. Users can continue to use the snapshots after the failover.If performance is a concern in your environment, we recommend that you create database snapshots only on secondary databases that are hosted by a secondary replica that is configured for manual failover mode.  If you ever manually fail over the availability group to this secondary replica, you can create a new set of database snapshots on another secondary replica, redirect clients to the new database snapshots, and drop all of the database snapshots from the now primary databases.  
  
## See Also  
 [Overview of Always On Availability Groups &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Database Snapshots &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
