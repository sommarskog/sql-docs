---
title: "Set a Trace Filter (Transact-SQL)"
description: "Set a Trace Filter (Transact-SQL)"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/06/2017"
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "filters [SQL Server], traces"
  - "traces [SQL Server], filters"
---
# Set a Trace Filter (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to use stored procedures to create a filter that retrieves only the information you need on an event being traced.  
  
### To set a trace filter  
  
1.  If the trace is already running, execute **sp_trace_setstatus** by specifying `@status = 0` to stop the trace.  
  
2.  Execute **sp_trace_setfilter** to configure the type of information to retrieve for the event being traced.  

> [!IMPORTANT]  
>  Unlike regular stored procedures, parameters of all [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] stored procedures (**sp_trace\__xx_**) are strictly typed and do not support automatic data type conversion. If these parameters are not called with the correct input parameter data types, as specified in the argument description, the stored procedure will return an error.  
  
## See Also  
 [Filter a Trace](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
