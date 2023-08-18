---
title: "sys.dm_tran_database_transactions (Transact-SQL)"
description: sys.dm_tran_database_transactions (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/19/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_tran_database_transactions"
  - "sys.dm_tran_database_transactions_TSQL"
  - "dm_tran_database_transactions_TSQL"
  - "sys.dm_tran_database_transactions"
helpviewer_keywords:
  - "sys.dm_tran_database_transactions dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Returns information about transactions at the database level.  
  
> [!NOTE]  
>  To call this DMV from [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use the name **sys.dm_pdw_nodes_tran_database_transactions**. [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)] 
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|ID of the transaction at the instance level, not the database level. It is only unique across all databases within an instance, but not unique across all server instances.|  
|database_id|**int**|ID of the database associated with the transaction. <br /><br />In [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], the values are unique within a single database or an elastic pool, but not within a logical server.|  
|database_transaction_begin_time|**datetime**|Time at which the database became involved in the transaction. Specifically, it is the time of the first log record in the database for the transaction.|  
|database_transaction_type|**int**|1 = Read/write transaction<br /><br /> 2 = Read-only transaction<br /><br /> 3 = System transaction|  
|database_transaction_state|**int**|1 = The transaction has not been initialized.<br /><br /> 3 = The transaction has been initialized but has not generated any log records.<br /><br /> 4 = The transaction has generated log records.<br /><br /> 5 = The transaction has been prepared.<br /><br /> 10 = The transaction has been committed.<br /><br /> 11 = The transaction has been rolled back.<br /><br /> 12 = The transaction is being committed. (The log record is being generated, but has not been materialized or persisted.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of log records generated in the database for the transaction.|  
|database_transaction_replicate_record_count|**int**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of log records generated in the database for the transaction that is replicated.|  
|database_transaction_log_bytes_used|**bigint**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of bytes used so far in the database log for the transaction.|  
|database_transaction_log_bytes_reserved|**bigint**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of bytes reserved for use in the database log for the transaction.|  
|database_transaction_log_bytes_used_system|**int**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of bytes used so far in the database log for system transactions on behalf of the transaction.|  
|database_transaction_log_bytes_reserved_system|**int**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Number of bytes reserved for use in the database log for system transactions on behalf of the transaction.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> Log sequence number (LSN) of the begin record for the transaction in the database log.|  
|database_transaction_last_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> LSN of the most recently logged record for the transaction in the database log.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> LSN of the most recent savepoint for the transaction in the database log.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> LSN of the commit log record for the transaction in the database log.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> LSN that was most recently rolled back to. If no rollback has taken place, the value is MaxLSN.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later.<br /><br /> LSN of the next record to undo.|  
|pdw_node_id|**int**|**Applies to**: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> The identifier for the node that this distribution is on.|  
  
## Permissions

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   

### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also  
 [sys.dm_tran_active_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Dynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transaction Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
