---
title: "sp_defaultdb (Transact-SQL)"
description: "sp_defaultdb (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_defaultdb_TSQL"
  - "sp_defaultdb"
helpviewer_keywords:
  - "sp_defaultdb"
dev_langs:
  - "TSQL"
---
# sp_defaultdb (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Changes the default database for a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) instead.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_defaultdb [ @loginame = ] 'login', [ @defdb = ] 'database'   
```  
  
## Arguments  
`[ @loginame = ] 'login'`
 Is the login name. *login* is **sysname**, with no default. *login* can be an existing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login or a Windows user or group. If a login for the Windows user or group does not exist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], it is automatically added.  
  
`[ @defdb = ] 'database'`
 Is the name of the new default database. *database* is **sysname**, with no default. *database* must already exist.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 **sp_defaultdb** calls ALTER LOGIN. This statement supports additional options. For information about changing default database, see [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_defaultdb** cannot be executed within a user-defined transaction.  
  
## Permissions  
 Requires ALTER ANY LOGIN permission.  
  
## Examples  
 The following example sets [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] as the default database for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login `Victoria`.  
  
```  
EXEC sp_defaultdb 'Victoria', 'AdventureWorks2022';  
```  
  
## See Also  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
