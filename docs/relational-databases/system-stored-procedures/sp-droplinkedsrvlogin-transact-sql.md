---
title: "sp_droplinkedsrvlogin (Transact-SQL)"
description: "sp_droplinkedsrvlogin (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_droplinkedsrvlogin_TSQL"
  - "sp_droplinkedsrvlogin"
helpviewer_keywords:
  - "sp_droplinkedsrvlogin"
dev_langs:
  - "TSQL"
---
# sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Removes an existing mapping between a login on the local server running [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and a login on the linked server.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## Arguments  
`[ @rmtsrvname = ] 'rmtsrvname'`
 Is the name of a linked server that the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login mapping applies to. *rmtsrvname* is **sysname**, with no default. *rmtsrvname* must already exist.  
  
`[ @locallogin = ] 'locallogin'`
 Is the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login on the local server that has a mapping to the linked server *rmtsrvname*. *locallogin* is **sysname**, with no default. A mapping for *locallogin* to *rmtsrvname* must already exist. If NULL, the default mapping created by **sp_addlinkedserver**, which maps all logins on the local server to logins on the linked server, is deleted.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 When the existing mapping for a login is deleted, the local server uses the default mapping created by **sp_addlinkedserver** when it connects to the linked server on behalf of that login. To change the default mapping, use **sp_addlinkedsrvlogin**.  
  
 If the default mapping is also deleted, only logins that have been explicitly given a login mapping to the linked server, by using **sp_addlinkedsrvlogin**, can access the linked server.  
  
 **sp_droplinkedsrvlogin** cannot be executed from within a user-defined transaction.  
  
## Permissions  
 Requires ALTER ANY LOGIN permission on the server.  
  
## Examples  
  
### A. Removing the login mapping for an existing user  
 The following example removes the mapping for the login `Mary` from the local server to the linked server `Accounts`. Therefore, login `Mary` uses the default login mapping.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### B. Removing the default login mapping  
 The following example removes the default login mapping originally created by executing `sp_addlinkedserver` on the linked server `Accounts`.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## See Also  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
