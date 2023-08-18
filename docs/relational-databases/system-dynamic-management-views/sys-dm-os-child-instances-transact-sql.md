---
title: "sys.dm_os_child_instances (Transact-SQL)"
description: sys.dm_os_child_instances (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_os_child_instances"
  - "sys.dm_os_child_instances_TSQL"
  - "dm_os_child_instances"
  - "dm_os_child_instances_TSQL"
helpviewer_keywords:
  - "server state information [SQL Server]"
  - "sys.dm_os_child_instances dynamic management view"
  - "monitoring server health"
dev_langs:
  - "TSQL"
monikerRange: ">=sql-server-2016||>=sql-server-linux-2017||>=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE [sql-asa-pdw](../../includes/applies-to-version/sql-asa-pdw.md)]

  Returns a row for each user instance that has been created from the parent server instance.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 The information returned from **sys.dm_os_child_instances** can be used to determine the state of each User Instance (heart_beat) and to obtain the pipe name (instance_pipe_name) that can be used to create a connection to the User Instance using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or SQLCmd. You can only connect to a User Instance after it has been started by an external process, such as a client application. SQL management tools cannot start a User Instance.  
  
> [!NOTE]  
> User Instances are a feature of [!INCLUDE[ssexpress-2012-md](../../includes/ssexpress-2012-md.md)] only.  

> [!NOTE]  
> To call this from [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use the name **sys.dm_pdw_nodes_os_child_instances**. [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
|Column|Data type|Description|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|The name of the user that this user instance was created for.|  
|owning_principal_sid|nvarchar(256)|SID (Security-Identifier) of the principal who owns this user instance. This matches Windows SID.|  
|owning_principal_sid_binary|varbinary(85)|Binary version of the SID for the user who owns the user Instance|  
|**instance_name**|**nvarchar(128)**|The name of this user instance.|  
|**instance_pipe_name**|**nvarchar(260)**|When a user instance is created, a named pipe is created for applications to connect to. This name can be used in a connect string to connect to this user instance.|  
|**os_process_id**|**Int**|The process number of the Windows process for this user instance.|  
|**os_process_creation_date**|**Datetime**|The date and time when this user instance process was last started.|  
|**heart_beat**|**nvarchar(5)**|Current state of this user instance; either ALIVE or DEAD.|  
|**pdw_node_id**|**int**|**Applies to**: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> The identifier for the node that this distribution is on.|  
  
## Permissions  
 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## Remarks  
 For more information about dynamic management view, see [Dynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.  
  
## See also  
 [User Instances for Non-Administrators](/previous-versions/sql/)  
  
