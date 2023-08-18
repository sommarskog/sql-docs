---
title: "sp_msx_defect (Transact-SQL)"
description: "sp_msx_defect (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_msx_defect"
  - "sp_msx_defect_TSQL"
helpviewer_keywords:
  - "sp_msx_defect"
dev_langs:
  - "TSQL"
---
# sp_msx_defect (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Removes the current server from multiserver operations.  
  
> [!CAUTION]  
>  **sp_msx_defect** edits the registry. Manual editing of the registry is not recommended because inappropriate or incorrect changes can cause serious configuration problems for your system. Therefore, only experienced users should use the Registry Editor program to edit the registry. For more information, see the documentation for Microsoft Windows.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## Arguments  
`[ @forced_defection = ] forced_defection`
 Specifies whether or not to force the defection to occur if the Master SQLServerAgent has been permanently lost due to an irreversibly corrupt **msdb** database, or no **msdb** database backup. *forced_defection*is **bit**, with a default of **0**, which indicates that no forced defection should occur. A value of **1** forces defection.  
  
 After forcing a defection by executing **sp_msx_defect**, a member of the **sysadmin** fixed server role at the Master SQLServerAgent must run the following command to complete the defection:  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 When **sp_msx_defect** properly completes, a message is returned.  
  
## Permissions  
 To execute this stored procedure, a user must be a member of the **sysadmin** fixed server role.  
  
## See Also  
 [sp_msx_enlist &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
