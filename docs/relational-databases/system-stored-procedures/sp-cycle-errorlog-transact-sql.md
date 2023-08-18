---
title: "sp_cycle_errorlog (Transact-SQL)"
description: "sp_cycle_errorlog (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_cycle_errorlog_TSQL"
  - "sp_cycle_errorlog"
helpviewer_keywords:
  - "sp_cycle_errorlog"
dev_langs:
  - "TSQL"
---
# sp_cycle_errorlog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Closes the current error log file and cycles the error log extension numbers just like a server restart. The new error log contains version and copyright information and a line indicating that the new log has been created.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_cycle_errorlog  
```  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 Every time [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is started, the current error log is renamed to **errorlog.1**; **errorlog.1** becomes **errorlog.2**, **errorlog.2** becomes **errorlog.3**, and so on. **sp_cycle_errorlog** enables you to cycle the error log files without stopping and starting the server.  
  
## Permissions  
 Execute permissions for **sp_cycle_errorlog** are restricted to members of the **sysadmin** fixed server role.  
  
## Examples  
 The following example cycles the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error log.  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
