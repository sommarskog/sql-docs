---
title: "sp_scriptpublicationcustomprocs (Transact-SQL)"
description: "sp_scriptpublicationcustomprocs (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_scriptpublicationcustomprocs"
  - "sp_scriptpublicationcustomprocs_TSQL"
helpviewer_keywords:
  - "sp_scriptpublicationcustomprocs"
dev_langs:
  - "TSQL"
---
# sp_scriptpublicationcustomprocs (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Scripts the custom INSERT, UPDATE, and DELETE procedures for all table articles in a publication in which the auto-generate custom procedure schema option is enabled. **sp_scriptpublicationcustomprocs** is particularly useful for setting up subscriptions for which the snapshot is applied manually.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_scriptpublicationcustomprocs [ @publication = ] 'publication_name'  
```  
  
## Arguments  
`[ @publication = ] 'publication_name'`
 Is the name of the publication. *publication_name* is **sysname** with no default.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 Returns a result set that consists of a single **nvarchar(4000)** column. The result set forms the complete CREATE PROCEDURE statement necessary to create the custom stored procedure.  
  
## Remarks  
 Custom procedures are not scripted for articles without the auto-generate custom procedure (0x2) schema option.  
  
 The following procedures are used by **sp_scriptpublicationcustomprocs** to create procedures the Subscriber and should not be executed directly:  
  
 **sp_script_reconciliation_delproc**  
  
 **sp_script_reconciliation_insproc**  
  
 **sp_script_reconciliation_vdelproc**  
  
 **sp_script_reconciliation_xdelproc**  
  
 **sp_scriptdelproc**  
  
 **sp_scriptinsproc**  
  
 **sp_scriptmappedupdproc**  
  
 **sp_scriptupdproc**  
  
 **sp_scriptvdelproc**  
  
 **sp_scriptvupdproc**  
  
 **sp_scriptxdelproc**  
  
 **sp_scriptxupdproc**  
  
## Permissions  
 Execute permission is granted to **public**; a procedural security check is performed inside this stored procedure to restrict access to members of the **sysadmin** fixed server role and **db_owner** fixed database role in current database.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
