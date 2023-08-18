---
title: "Modify an Existing Trace (Transact-SQL)"
description: "Modify an Existing Trace (Transact-SQL)"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/06/2017"
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "traces [SQL Server], modifying"
  - "modifying traces"
---
# Modify an Existing Trace (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to use stored procedures to modify an existing trace.  
  
### To modify an existing trace  
  
1.  If the trace is already running, execute **sp_trace_setstatus** by specifying **@status = 0** to stop the trace.  
  
2.  To modify trace events, execute **sp_trace_setevent** by specifying the changes through the parameters. Listed in order, the parameters are:  

    -   **\@traceid** (Trace ID)  
  
    -   **\@eventid** (Event ID)  
  
    -   **\@columnid** (Column ID)  
  
    -   **\@on** (ON)  
  
     When you modify the **\@on** parameter, keep in mind its interaction with the **\@columnid** parameter:  
  
    |ON|Column ID|Result|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|Event is turned on. All columns are cleared.|  
    ||NOT NULL|Column is turned on for the specified event.|  
    |OFF (**0**)|NULL|Event is turned off. All columns are cleared.|  
    ||NOT NULL|Column is turned off for the specified event.|  
  
> [!IMPORTANT]
>  Unlike regular stored procedures, parameters of all [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] stored procedures (<strong>sp_trace_*xx*</strong>) are strictly typed and do not support automatic data type conversion. If these parameters are not called with the correct input parameter data types, as specified in the argument description, the stored procedure returns an error.  
  
## See Also  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
