---
title: "sp_dropremotelogin (Transact-SQL)"
description: "sp_dropremotelogin (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_dropremotelogin"
  - "sp_dropremotelogin_TSQL"
helpviewer_keywords:
  - "sp_dropremotelogin"
dev_langs:
  - "TSQL"
---
# sp_dropremotelogin (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Removes a remote login mapped to a local login used to execute remote stored procedures against the local server running [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use linked servers and linked-server stored procedures instead.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## Arguments  
`[ @remoteserver = ] 'remoteserver'`
 Is the name of the remote server mapped to the remote login that is to be removed. *remoteserver* is **sysname**, with no default. *remoteserver* must already exist.  
  
`[ @loginame = ] 'login'`
 Is the optional login name on the local server that is associated with the remote server. *login* is **sysname**, with a default of NULL. *login* must already exist if specified.  
  
`[ @remotename = ] 'remote_name'`
 Is the optional name of the remote login that is mapped to *login* when logging in from the remote server. *remote_name* is **sysname**, with a default of NULL.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 If only *remoteserver* is specified, all remote logins for that remote server are removed from the local server. If *login* is also specified, all remote logins from *remoteserver* mapped to that specific local login are removed from the local server. If *remote_name* is also specified, only the remote login for that remote user from *remoteserver* is removed from the local server.  
  
 To add local server users, use **sp_addlogin**. To remove local server users, use **sp_droplogin**.  
  
 Remote logins are required only when you use earlier versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] version 7.0 and later versions use linked server logins instead. Use **sp_addlinkedsrvlogin** and **sp_droplinkedsrvlogin** to add and remove linked server logins.  
  
 **sp_dropremotelogin** cannot be executed within a user-defined transaction.  
  
## Permissions  
 Requires membership in the **sysadmin** or **securityadmin** fixed server roles.  
  
## Examples  
  
### A. Dropping all remote logins for a remote server  
 The following example removes the entry for the remote server `ACCOUNTS`, and, therefore, removes all mappings between logins on the local server and remote logins on the remote server.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### B. Dropping a login mapping  
 The following example removes the entry for mapping remote logins from the remote server `ACCOUNTS` to the local login `Albert`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### C. Dropping a remote user  
 The following example removes the login for the remote login `Chris` on the remote server `ACCOUNTS` that was mapped to the local login `salesmgr`.  
  
```sql
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## See Also  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
