---
title: "sp_helpmergefilter (Transact-SQL)"
description: "sp_helpmergefilter (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_helpmergefilter"
  - "sp_helpmergefilter_TSQL"
helpviewer_keywords:
  - "sp_helpmergefilter"
dev_langs:
  - "TSQL"
---
# sp_helpmergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information about merge filters. This stored procedure is executed at the Publisher on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the name of the publication. *publication* is **sysname**, with no default.  
  
`[ @article = ] 'article'`
 Is the name of the article. *article* is **sysname**, with a default of **%**, which returns the names of all articles.  
  
`[ @filtername = ] 'filtername'`
 Is the name of the filter about which to return information. *filtername* is **sysname**, with a default of **%**, which returns information about all the filters defined on the article or publication.  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**int**|ID of the join filter.|  
|**filtername**|**sysname**|Name of the filter.|  
|**join article name**|**sysname**|Name of the join article.|  
|**join_filterclause**|**nvarchar(2000)**|Filter clause qualifying the join.|  
|**join_unique_key**|**int**|Whether the join is on a unique key.|  
|**base table owner**|**sysname**|Name of the owner of the base table.|  
|**base table name**|**sysname**|Name of the base table.|  
|**join table owner**|**sysname**|Name of the owner of the table being joined to the base table.|  
|**join table name**|**sysname**|Name of the table being joined to the base table.|  
|**article name**|**sysname**|Name of the table article being joined to the base table.|  
|**filter_type**|**tinyint**|Type of merge filter, which can be one of the following:<br /><br /> **1** = join filter only<br /><br /> **2** = logical record relationship<br /><br /> **3** = both|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_helpmergefilter** is used in merge replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role and the **db_owner** fixed database role can execute **sp_helpmergefilter**.  
  
## See Also  
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
