---
title: "sp_grant_publication_access (Transact-SQL)"
description: "sp_grant_publication_access (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_grant_publication_access_TSQL"
  - "sp_grant_publication_access"
helpviewer_keywords:
  - "sp_grant_publication_access"
dev_langs:
  - "TSQL"
---
# sp_grant_publication_access (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Adds a login to the access list of the publication. This stored procedure is executed at the Publisher on the publication database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
sp_grant_publication_access [ @publication = ] 'publication', [ @login = ] 'login'   
    [ , [ @reserved = ] 'reserved' ]  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the name of the publication to access. **'***publication***'** is **sysname**, with no default.  
  
`[ @login = ] 'login'`
 Is the login ID. **'***login***'** is **sysname**, with no default.  
  
`[ @reserved = ] 'reserved'`
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_grant_publication_access** is used in snapshot, transactional, and merge replication.  
  
 This stored procedure can be called repeatedly.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_grant_publication_access**.  
  
## See Also  
 [sp_help_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Secure the Publisher](../../relational-databases/replication/security/secure-the-publisher.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
