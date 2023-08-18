---
title: "sys.dm_server_services (Transact-SQL)"
description: sys.dm_server_services (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_server_services"
  - "sys.dm_server_services"
  - "sys.dm_server_services_TSQL"
  - "dm_server_services_TSQL"
helpviewer_keywords:
  - "sys.dm_server_services dynamic management view"
dev_langs:
  - "TSQL"
---
# sys.dm_server_services (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information about the SQL Server, Full-Text, SQL Server Launchpad service (SQL Server 2017+), and SQL Server Agent services in the current instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use this dynamic management view to report status information about these services.  
  
 
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|Name of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], Full-text, or SQL Server Agent service. Cannot be null.|  
|startup_type|**int**|Indicates the start mode of the service. The following are the possible values and their corresponding descriptions.<br /><br /> 0: Other<br />1: Other<br />2: Automatic<br />3: Manual<br />4: Disabled<br /><br /> Is nullable.|  
|startup_type_desc|**nvarchar(256)**|Describes the start mode of the service. The following are the possible values and their corresponding descriptions.<br /><br /> Other: Other (boot start)<br />Other: Other (system start)<br />Automatic: Auto start<br />Manual: Demand start<br />Disabled: Disabled<br /><br /> Cannot be null.|  
|status|**int**|Indicates the current status of the service. The following are the possible values and their corresponding descriptions.<br /><br /> 1: Stopped<br />2: Other (start pending)<br />3: Other (stop pending)<br />4: Running<br />5: Other (continue pending)<br />6: Other (pause pending)<br />7: Paused<br /><br /> Is nullable.|  
|status_desc|**nvarchar(256)**|Describes the current status of the service. The following are the possible values and their corresponding descriptions.<br /><br /> Stopped: The service is stopped.<br />Other (start operation pending): The service is in the process of starting.<br />Other (stop operation pending): The service is in the process of stopping.<br />Running: The service is running.<br />Other (continue operations pending): The service is in a pending state.<br />Other (pause pending): The service is in the process of pausing.<br />Paused: The service is paused.<br /><br /> Cannot be null.|  
|process_id|**int**|The process ID of the service. Cannot be null.|  
|last_startup_time|**datetimeoffset(7)**|The date and time the service was last started. Is nullable.|  
|service_account|**nvarchar(256)**|The account authorized to control the service. This account can start or stop the service, or modify service properties. Cannot be null.|  
|filename|**nvarchar(256)**|The path and filename of the service executable. Cannot be null.|  
|is_clustered|**nvarchar(1)**|Indicates whether the service is installed as a resource of a clustered server. Cannot be null.|  
|cluster_nodename|**nvarchar(256)**|The name of the cluster node on which the service is installed. Is nullable.|
|instant_file_initialization_enabled|**nvarchar(1)**|Specifies whether instant file initialization is enabled for the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] service.<br /><br />Y = instant file initialization is enabled for the service.<br /><br />N = instant file initialization is disabled for the service.<br /><br /> Is nullable.<br /><br /> **Note:** Does not apply to other services such as the SQL Server Agent.<br /><br /> **Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4, and [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] SP1 and later).|  
  
## Permissions  
 Requires `VIEW SERVER STATE` permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER SECURITY STATE permission on the server.

## See also  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
