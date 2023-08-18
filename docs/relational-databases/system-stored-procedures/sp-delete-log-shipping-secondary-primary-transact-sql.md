---
title: "sp_delete_log_shipping_secondary_primary (Transact-SQL)"
description: "sp_delete_log_shipping_secondary_primary (Transact-SQL)"
author: MashaMSFT
ms.author: mathoma
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_delete_log_shipping_secondary_primary_TSQL"
  - "sp_delete_log_shipping_secondary_primary"
helpviewer_keywords:
  - "sp_delete_log_shipping_secondary_primary"
dev_langs:
  - "TSQL"
---
# sp_delete_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  This stored procedure removes the information about the specified primary server from the secondary server, and removes the copy job and restore job from the secondary.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_delete_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server'  
[ @primary_database = ] 'primary_database'  
```  
  
## Arguments  
`[ @primary_server = ] 'primary_server'`
 The name of the primary instance of the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in the log shipping configuration. *primary_server* is **sysname** and cannot be NULL.  
  
`[ @primary_database = ] 'primary_database'`
 Is the name of the database on the primary server. *primary_database* is **sysname**, with no default.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
 None.  
  
## Remarks  
 **sp_delete_log_shipping_secondary_primary** must be run from the **master** database on the secondary server. This stored procedure does the following:  
  
1.  Deletes the copy and restore jobs for the secondary ID.  
  
2.  Deletes the entry in **log_shipping_secondary**.  
  
3.  Calls **sp_delete_log_shipping_alert_job** on the monitor server.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can run this procedure.  
  
## See Also  
 [About Log Shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
