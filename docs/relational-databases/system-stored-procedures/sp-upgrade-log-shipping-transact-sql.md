---
title: "sp_upgrade_log_shipping (Transact-SQL)"
description: "sp_upgrade_log_shipping (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_upgrade_log_shipping"
  - "sp_upgrade_log_shipping_TSQL"
helpviewer_keywords:
  - "sp_upgrade_log_shipping"
dev_langs:
  - "TSQL"
---
# sp_upgrade_log_shipping (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The sp_upgrade_log_shipping stored procedure is invoked automatically for upgrading metadata that is specific to log shipping.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_upgrade_log_shipping  
```  
  
## Arguments  
 None.  
  
## Return Code Values  
 0 (success) or 1 (otherwise)  
  
## Result Sets  
 None.  
  
## Remarks  
 This stored procedure is invoked automatically during [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] upgrade for upgrading metadata for log shipping. You do not need to execute this procedure explicitly, unless a problem occurs with the metadata during upgrade.  
  
 sp_upgrade_log_shipping must be run from the master database on the primary, secondary, or monitor server.  
  
## Permissions  
 Requires membership in the **sysadmin** fixed server role.  
  
## See Also  
 [About Log Shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
