---
title: "sp_helprolemember (Transact-SQL)"
description: "sp_helprolemember (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_helprolemember_TSQL"
  - "sp_helprolemember"
helpviewer_keywords:
  - "sp_helprolemember"
dev_langs:
  - "TSQL"
---
# sp_helprolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information about the direct members of a role in the current database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## Arguments  
`[ @rolename = ] ' role '`
 Is the name of a role in the current database. *role* is **sysname**, with a default of NULL. *role* must exist in the current database. If *role* is not specified, then all roles that contain at least one member from the current database are returned.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|Name of the role in the current database.|  
|**MemberName**|**sysname**|Name of a member of **DbRole.**|  
|**MemberSID**|**varbinary(85)**|Security identifier of **MemberName.**|  
  
## Remarks  
 If the database contains nested roles, **MemberName** may be the name of a role. **sp_helprolemember** does not show membership obtained through nested roles. For example if User1 is a member of Role1, and Role1 is a member of Role2, `EXEC sp_helprolemember 'Role2'`; will return Role1, but not the members of Role1 (User1 in this example). To return nested memberships, you must execute **sp_helprolemember** repeatedly for each nested role.  
  
 Use **sp_helpsrvrolemember** to display the members of a fixed server role.  
  
 Use [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md) to check role membership for a specified user.  
  
## Permissions  
 Requires membership in the **public** role.  
  
## Examples  
 The following example displays the members of the `Sales` role.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## See Also  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
