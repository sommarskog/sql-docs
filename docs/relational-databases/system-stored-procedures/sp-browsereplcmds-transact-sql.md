---
title: "sp_browsereplcmds (Transact-SQL)"
description: "sp_browsereplcmds (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_browsereplcmds_TSQL"
  - "sp_browsereplcmds"
helpviewer_keywords:
  - "sp_browsereplcmds"
dev_langs:
  - "TSQL"
---
# sp_browsereplcmds (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Returns a result set in a readable version of the replicated commands stored in the distribution database, and is used as a diagnostic tool. This stored procedure is executed at the Distributor on the distribution database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_browsereplcmds [ [ @xact_seqno_start = ] 'xact_seqno_start' ]  
    [ , [ @xact_seqno_end = ] 'xact_seqno_end' ]   
    [ , [ @originator_id = ] 'originator_id' ]  
    [ , [ @publisher_database_id = ] 'publisher_database_id' ]  
    [ , [ @article_id = ] 'article_id' ]  
    [ , [ @command_id= ] command_id ]  
    [ , [ @agent_id = ] agent_id ]  
    [ , [ @compatibility_level = ] compatibility_level ]  
```  
  
## Arguments  
`[ @xact_seqno_start = ] 'xact_seqno_start'`
 Specifies the lowest valued exact sequence number to return. *xact_seqno_start* is **nchar(22)**, with a default of 0x00000000000000000000.  
  
`[ @xact_seqno_end = ] 'xact_seqno_end'`
 Specifies the highest exact sequence number to return. *xact_seqno_end* is **nchar(22)**, with a default of 0xFFFFFFFFFFFFFFFFFFFF.  
  
`[ @originator_id = ] 'originator_id'`
 Specifies if commands with the specified *originator_id* are returned. *originator_id* is **int**, with a default of NULL.  
  
`[ @publisher_database_id = ] 'publisher_database_id'`
 Specifies if commands with the specified *publisher_database_id* are returned. *publisher_database_id* is **int**, with a default of NULL.  
  
`[ @article_id = ] 'article_id'`
 Specifies if commands with the specified *article_id* are returned. *article_id* is **int**, with a default of NULL.  
  
`[ @command_id = ] command_id`
 Is the location of the command in [MSrepl_commands &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msrepl-commands-transact-sql.md) to be decoded. *command_id* is **int**, with a default of NULL. If specified, all other parameters must be specified also, and *xact_seqno_start*must be identical to *xact_seqno_end*.  
  
`[ @agent_id = ] agent_id`
 Specifies that only commands for a specific replication agent are returned. *agent_id* is **int**, with a default value of NULL.  
  
`[ @compatibility_level = ] compatibility_level`
 Is the version of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on which the *compatibility_level* is **int**, with a default value of 9000000.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**varbinary(16)**|Sequence number of the command.|  
|**originator_srvname**|**sysname**|Server where the transaction originated.|  
|**originator_db**|**sysname**|Database where the transaction originated.|  
|**article_id**|**int**|ID of the article.|  
|**type**|**int**|Type of command.|  
|**partial_command**|**bit**|Indicates whether this is a partial command.|  
|**hashkey**|**int**|Internal use only.|  
|**originator_publication_id**|**int**|ID of the publication where the transaction originated.|  
|**originator_db_version**|**int**|Version of the database where the transaction originated.|  
|**originator_lsn**|**varbinary(16)**|Identifies the log sequence number (LSN) for the command in the originating publication. Used in peer-to-peer transactional replication.|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] command.|  
|**command_id**|**int**|ID of the command in [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
  
 Long commands can be split across several rows in the result sets.  
  
## Remarks  
 **sp_browsereplcmds** is used in transactional replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or members of the **db_owner** or **replmonitor** fixed database roles on the distribution database can execute **sp_browsereplcmds**.  
  
## See Also  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
