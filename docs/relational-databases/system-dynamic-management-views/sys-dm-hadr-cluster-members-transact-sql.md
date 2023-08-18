---
title: "sys.dm_hadr_cluster_members (Transact-SQL)"
description: sys.dm_hadr_cluster_members (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_hadr_cluster_members_TSQL"
  - "sys.dm_hadr_cluster_members"
  - "dm_hadr_cluster_members_TSQL"
  - "dm_hadr_cluster_members"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "Availability Groups [SQL Server], WSFC clusters"
  - "sys.dm_hadr_cluster_members catalog view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017"
---
# sys.dm_hadr_cluster_members (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  If the WSFC node that hosts a local instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that is enabled for [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] has WSFC quorum, returns a row for each of the members that constitute the quorum and the state of each of them. This includes of all nodes in the cluster (returned with CLUSTER_ENUM_NODE type by the **Clusterenum** function) and the disk or file-share witness, if any. The row returned for a given member contains information about the state of that member. For example, for a five node cluster with majority node quorum in which one node is down, when **sys.dm_hadr_cluster_members** is queried from a server instance that is that is enabled for [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] that resides on a node with quorum, **sys.dm_hadr_cluster_members** reflects the state of the down node as "NODE_DOWN".  
  
 If the WSFC node has no quorum, no rows are returned.  
  
 Use this dynamic management view to answer the following questions:  
  
-   What nodes are currently running on the WSFC cluster?  
  
-   How many more failures can the WSFC cluster tolerate before losing quorum in a majority-node case?  

 > [!TIP]
 > Beginning in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], this dynamic management view supports Always On Failover Cluster Instances in addition to Always On Availability Groups.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|Member name, which can be a computer name, a drive letter, or a file share path.|  
|**member_type**|**tinyint**|The type of member, one of:<br /><br /> 0 = WSFC node<br /><br /> 1 = Disk witness<br /><br /> 2 = File share witness<br /><br /> 3 = Cloud Witness|  
|**member_type_desc**|**nvarchar(50)**|Description of **member_type**, one of:<br /><br /> CLUSTER_NODE<br /><br /> DISK_WITNESS<br /><br /> FILE_SHARE_WITNESS<br /><br /> CLOUD_WITNESS|  
|**member_state**|**tinyint**|The member state, one of:<br /><br /> 0 = Offline<br /><br /> 1 = Online|  
|**member_state_desc**|**nvarchar(60)**|Description of **member_state**, one of:<br /><br /> UP<br /><br /> DOWN|  
|**number_of_quorum_votes**|**tinyint**|Number of quorum votes possessed by this quorum member. For No Majority: Disk Only quorums, this value defaults to 0. For other quorum types, this value defaults to 1.|  
  
## Permissions  
 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.
  
## See also  
 [Always On Availability Groups Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On Availability Groups Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitor Availability Groups &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On Availability Groups &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
