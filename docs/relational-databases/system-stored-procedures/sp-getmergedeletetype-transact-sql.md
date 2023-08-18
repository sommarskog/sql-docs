---
title: "sp_getmergedeletetype (Transact-SQL)"
description: "sp_getmergedeletetype (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_getmergedeletetype"
  - "sp_getmergedeletetype_TSQL"
helpviewer_keywords:
  - "sp_getmergedeletetype"
dev_langs:
  - "TSQL"
---
# sp_getmergedeletetype (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns the type of merge delete. This stored procedure is executed at the Publisher on the publication database or at the Subscriber on the subscription database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## Arguments  
`[ @source_object = ] 'source_object'`
 Is the name of the source object. *source_object* is **nvarchar(386)**, with no default.  
  
`[ @rowguid = ] 'rowguid'`
 Is the row identifier for the delete type. *rowguid* is **uniqueidentifier**, with no default.  
  
`[ @delete_type = ] delete_type OUTPUT`
 Is the code indicating the type of delete. *delete_type* is **int**, with no default. *delete_type* is also an OUTPUT parameter, and can be one of these values.  
  
|Value|Description|  
|-----------|-----------------|  
|**1**|User delete|  
|**5**|Partial delete|  
|**6**|System delete|  
  
## Remarks  
 **sp_getmergedeletetype** is used in merge replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_getmergedeletetype**.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
