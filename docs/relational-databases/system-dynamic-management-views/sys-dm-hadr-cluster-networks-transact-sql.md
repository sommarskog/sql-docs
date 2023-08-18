---
title: "sys.dm_hadr_cluster_networks (Transact-SQL)"
description: sys.dm_hadr_cluster_networks (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_hadr_cluster_networks"
  - "sys.dm_hadr_cluster_networks_TSQL"
  - "sys.dm_hadr_cluster_networks"
  - "dm_hadr_cluster_networks_TSQL"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "Availability Groups [SQL Server], WSFC clusters"
  - "sys.dm_hadr_cluster_networks dynamic management view"
dev_langs:
  - "TSQL"
---
# sys.dm_hadr_cluster_networks (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns a row for every WSFC cluster member that is participating in an availability group's subnet configuration. You can use this dynamic management view to validate the network virtual IP that is configured for each availability replica.  
  
 Primary key:  **member_name** + **network_subnet_IP** + **network_subnet_prefix_length**  
  
 > [!TIP]
 > Beginning in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], this dynamic management view supports Always On Failover Cluster Instances in addition to Always On Availability Groups.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**member_name**|**nvarchar(128)**|A computer name of a node in the WSFC cluster.|  
|**network_subnet_ip**|**nvarchar(48)**|Network IP address of the subnet to which the computer belongs. This can be an IPv4 or IPv6 address.|  
|**network_subnet_ipv4_mask**|**nvarchar(45)**|Network subnet mask that specifies the subnet to which the IP address belongs. **network_subnet_ipv4_mask** to specify the DHCP <network_subnet_option> options in a WITH DHCP clause of the [CREATE AVAILABILITY GROUP](../../t-sql/statements/create-availability-group-transact-sql.md) or [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] statement.<br /><br /> NULL = IPv6 subnet.|  
||||  
|**network_subnet_prefix_length**|**int**|Network IP prefix length that specifies the subnet to which the computer belongs.|  
|**is_public**|**bit**|Whether the network is private or public on the WSFC cluster, one of:<br /><br /> 0 = Private<br /><br /> 1 = Public|  
|**is_ipv4**|**bit**|Type of the subnet, one of:<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|   
  
## Permissions  
 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also  
 [Failover Clustering and Always On Availability Groups &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Monitor Availability Groups &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [sys.dm_os_cluster_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Querying the SQL Server System Catalog FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.yml)   
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
