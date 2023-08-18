---
title: "sp_deletepeerrequesthistory (Transact-SQL)"
description: "sp_deletepeerrequesthistory (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_deletepeerrequesthistory"
  - "sp_deletepeerrequesthistory_TSQL"
helpviewer_keywords:
  - "sp_deletepeerrequesthistory"
dev_langs:
  - "TSQL"
---
# sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Deletes history related to a publication status request, which includes the request history ([MSpeer_request &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) as well as the response history ([MSpeer_response &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md)).This stored procedure is executed on the publication database at a Publisher participating in a Peer-to-Peer replication topology. For more information, see [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Name of the publication for which the status request was made. *publication* is **sysname**, with no default.  
  
`[ @request_id = ] request_id`
 Specifies an individual status request so that all responses to this request will be deleted. *request_id* is **int**, with a default value of NULL.  
  
`[ @cutoff_date = ] cutoff_date`
 Specifies a cutoff date, before which all earlier response records are deleted. *cutoff_date* is **datetime**, with a default value of NULL.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_deletepeerrequesthistory** is used in a Peer-to-Peer transactional replication topology. For more information, see [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 When executing **sp_deletepeerrequesthistory**, either *request_id* or *cutoff_date* must be specified.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute **sp_deletepeerrequesthistory**.  
  
## See Also  
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
