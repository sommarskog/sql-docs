---
title: "sp_refreshsubscriptions (Transact-SQL)"
description: "sp_refreshsubscriptions (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_refreshsubscriptions"
  - "sp_refreshsubscriptions_TSQL"
helpviewer_keywords:
  - "sp_refreshsubscriptions"
dev_langs:
  - "TSQL"
---
# sp_refreshsubscriptions (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Add subscriptions to new articles for all the existing Subscribers to an immediate-updating publication. This stored procedure is executed at the Publisher on the publication database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_refreshsubscriptions [ @publication = ] 'publication'  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the publication for which to refresh subscriptions. *publication* is **sysname**, with no default.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 **sp_refreshsubscriptions** is used in snapshot, transactional, and merge replication.  
  
 **sp_refreshsubscriptions** is called by **sp_addarticle** for an immediate-updating publication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_refreshsubscriptions**.  
  
## See Also  
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
