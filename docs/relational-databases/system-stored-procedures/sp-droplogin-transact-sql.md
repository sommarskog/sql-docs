---
title: "sp_droplogin (Transact-SQL)"
description: "sp_droplogin (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_droplogin"
  - "sp_droplogin_TSQL"
helpviewer_keywords:
  - "sp_droplogin"
dev_langs:
  - "TSQL"
---
# sp_droplogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Removes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login. This prevents access to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] under that login name.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) instead.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_droplogin [ @loginame = ] 'login'  
```  
  
## Arguments  
`[ @loginame = ] 'login'`
 Is the login to be removed. *login* is **sysname**, with no default. *login* must already exist in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 **sp_droplogin** calls DROP LOGIN.  
  
 **sp_droplogin** cannot be executed within a user-defined transaction.  
  
## Permissions  
 Requires ALTER ANY LOGIN permission on the server.  
  
## Examples  
 The following example uses `DROP LOGIN` to remove the login `Victoria` from an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. This is the preferred method.  
  
```  
DROP LOGIN Victoria;  
GO  
```  
  
## See Also  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
