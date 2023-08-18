---
title: "sp_dbmmonitordropmonitoring (Transact-SQL)"
description: "sp_dbmmonitordropmonitoring (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_dbmmonitordropmonitoring_TSQL"
  - "sp_dbmmonitordropmonitoring"
helpviewer_keywords:
  - "sp_dbmmonitordropmonitoring"
  - "database mirroring [SQL Server], monitoring"
dev_langs:
  - "TSQL"
---
# sp_dbmmonitordropmonitoring (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Stops and deletes the mirroring monitor job for all the databases on the server instance.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_dbmmonitordropmonitoring   
```  
  
## Arguments  
 None  
  
## Return Code Values  
 None  
  
## Result Sets  
 None  
  
## Permissions  
 Requires membership in the **sysadmin** fixed server role.  
  
## Examples  
 The following example drops database mirroring monitoring on all of the mirrored databases on the server instance.  
  
```  
EXEC sp_dbmmonitordropmonitoring ;  
```  
  
## See Also  
 [Monitoring Database Mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
