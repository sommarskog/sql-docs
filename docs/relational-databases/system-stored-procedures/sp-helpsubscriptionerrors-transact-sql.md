---
title: "sp_helpsubscriptionerrors (Transact-SQL)"
description: "sp_helpsubscriptionerrors (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_helpsubscriptionerrors_TSQL"
  - "sp_helpsubscriptionerrors"
helpviewer_keywords:
  - "sp_helpsubscriptionerrors"
dev_langs:
  - "TSQL"
---
# sp_helpsubscriptionerrors (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Returns all transactional replication errors for a given subscription. This stored procedure is executed at the Distributor on the distribution database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the name of the Publisher. *publisher* is **sysname**, with no default.  
  
`[ @publisher_db = ] 'publisher_db'`
 Is the name of the publication database. *publisher_db* is **sysname**, with no default.  
  
`[ @publication = ] 'publication'`
 Is the name of the publication. *publication* is **sysname**, with no default.  
  
`[ @subscriber = ] 'subscriber'`
 Is the name of the Subscriber. *subscriber* is **sysname**, with no default.  
  
`[ @subscriber_db = ] 'subscriber_db'`
 Is the name of the subscription database. *subscriber_db* is **sysname**, with no default.  
  
## Result Set  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID of the error.|  
|**time**|**datetime**|Time the error occurred.|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|Error source type ID.|  
|**source_name**|**nvarchar(100)**|Name of the error source.|  
|**error_code**|**sysname**|Error code.|  
|**error_text**|**ntext**|Error message.|  
|**xact_seqno**|**varbinary(16)**|Starting transaction log sequence number of the failed execution batch. Used only by the Distribution Agents, this is the transaction log sequence number of the first transaction in the failed execution batch.|  
|**command_id**|**int**|Command ID of the failed execution batch. Used only by the Distribution Agents, this is the command ID of the first command in the failed execution batch.|  
|**session_id**|**int**|ID of the agent session in which the error occurred.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_helpsubscriptionerrors** is used with snapshot and transactional replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute **sp_helpsubscriptionerrors**.  
  
## See Also  
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
