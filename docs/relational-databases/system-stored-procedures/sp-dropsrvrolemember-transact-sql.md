---
title: "sp_dropsrvrolemember (Transact-SQL)"
description: "sp_dropsrvrolemember (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/20/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_dropsrvrolemember"
  - "sp_dropsrvrolemember_TSQL"
helpviewer_keywords:
  - "sp_dropsrvrolemember"
dev_langs:
  - "TSQL"
---
# sp_dropsrvrolemember (Transact-SQL)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Removes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login or a Windows user or group from a fixed server role.

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) instead.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## Arguments

**[ @loginame = ]** '_login_'  
Is the name of a login to remove from the fixed server role. *login* is **sysname**, with no default. *login* must exist.  

**[ @rolename = ]** '_role_'  
Is the name of a server role. *role* is **sysname**, with a default of NULL. *role* must be one of the following values:  

-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 Only sp_dropsrvrolemember can be used to remove a login from a fixed server role. Use sp_droprolemember to remove a member from a database role.  
  
 The sa login cannot be removed from any fixed server role.  
  
 sp_dropsrvrolemember cannot be executed within a user-defined transaction.  
  
## Permissions  
 Requires membership in the sysadmin fixed server role, or both ALTER ANY LOGIN permission on the server and membership in the role from which the member is being dropped.  
  
## Examples  
 The following example removes the login `JackO` from the `sysadmin` fixed server role.  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## See Also  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Security Functions &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
