---
title: "sp_delete_targetsvrgrp_member (Transact-SQL)"
description: "sp_delete_targetsvrgrp_member (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_delete_targetsvrgrp_member_TSQL"
  - "sp_delete_targetsvrgrp_member"
helpviewer_keywords:
  - "sp_delete_targetsvrgrp_member"
dev_langs:
  - "TSQL"
---
# sp_delete_targetsvrgrp_member (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Removes a target server from a target server group.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_delete_targetsvrgrp_member [ @group_name = ] 'group_name' , [ server_name = ] 'server_name'   
```  
  
## Arguments  
`[ @group_name = ] 'group_name'`
 The name of the group. *group_name* is **sysname**, with no default.  
  
`[ @server_name = ] 'server_name'`
 The name of the server to remove from the specified group. *server_name* is **nvarchar(30)**, with no default.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 None  
  
## Permissions  
 To run this stored procedure, users must be granted the **sysadmin** fixed server role.  
  
## Examples  
 The following example removes the server `LONDON1` from the Servers Maintaining Customer Information group.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetsvrgrp_member   
    @group_name = N'Servers Maintaining Customer Information',  
    @server_name = N'LONDON1';  
GO  
```  
  
## See Also  
 [sp_add_targetsvrgrp_member &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-targetsvrgrp-member-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
