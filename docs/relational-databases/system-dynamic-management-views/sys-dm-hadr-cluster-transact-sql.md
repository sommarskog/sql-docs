---
title: "sys.dm_hadr_cluster (Transact-SQL)"
description: sys.dm_hadr_cluster (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_hadr_cluster"
  - "dm_hadr_cluster_HADR"
  - "sys.dm_hadr_cluster_TSQL"
  - "dm_hadr_cluster"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "sys.dm_hadr_cluster catalog view"
  - "Availability Groups [SQL Server], WSFC clusters"
dev_langs:
  - "TSQL"
---
# sys.dm_hadr_cluster (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  If the Windows Server Failover Clustering (WSFC) node that hosts an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that is enabled for [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] has WSFC quorum, **sys.dm_hadr_cluster** returns a row that exposes the cluster name and information about the quorum. If the WSFC node has no quorum, no row is returned.  
 > [!TIP]
 > Beginning in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], this dynamic management view supports Always On Failover Cluster Instances in addition to Always On Availability Groups.

|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**cluster_name**|**nvarchar(128)**|Name of the WSFC cluster that hosts the instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that are enabled for [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**quorum_type**|**tinyint**|Type of quorum used by this WSFC cluster, one of:<br /><br /> 0 = Node Majority. This quorum configuration can sustain failures of half the nodes (rounding up) minus one. For example, on a seven node cluster, this quorum configuration can sustain three node failures.<br /><br /> 1 = Node and Disk Majority. If the disk witness remains on line, this quorum configuration can sustain failures of half the nodes (rounding up). For example, a six node cluster in which the disk witness is online could sustain three node failures. If the disk witness goes offline or fails, this quorum configuration can sustain failures of half the nodes (rounding up) minus one. For example, a six node cluster with a failed disk witness could sustain two (3-1=2) node failures.<br /><br /> 2 = Node and File Share Majority. This quorum configuration works in a similar way to Node and Disk Majority, but uses a file-share witness instead of a disk witness.<br /><br /> 3 = No Majority: Disk Only. If the quorum disk is online, this quorum configuration can sustain failures of all nodes except one.<br /><br /> 4 = Unknown Quorum. Unknown Quorum for the cluster.<br /><br /> 5 = Cloud Witness. Cluster utilizes Microsoft Azure for quorum arbitration. If the cloud witness is available, the cluster can sustain the failure of half the nodes (rounding up).|  
|**quorum_type_desc**|**varchar(50)**|Description of **quorum_type**, one of:<br /><br /> NODE_MAJORITY<br /><br /> NODE_AND_DISK_MAJORITY<br /><br /> NODE_AND_FILE_SHARE_MAJORITY<br /><br /> NO_MAJORITY:_DISK_ONLY <br /><br /> UNKNOWN_QUORUM <br /><br /> CLOUD_WITNESS|  
|**quorum_state**|**tinyint**|State of the WSFC quorum, one of:<br /><br /> 0 = Unknown quorum state<br /><br /> 1 = Normal quorum<br /><br /> 2 = Forced quorum|  
|**quorum_state_desc**|**varchar(50)**|Description of **quorum_state**, one of:<br /><br /> UNKNOWN_QUORUM_STATE<br /><br /> NORMAL_QUORUM<br /><br /> FORCED_QUORUM|  
  
## Permissions  
 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also  
 [Always On Availability Groups Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On Availability Groups Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitor Availability Groups &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql.md)  
  
  
