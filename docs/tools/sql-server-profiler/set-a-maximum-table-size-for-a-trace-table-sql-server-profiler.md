---
title: Set a Maximum Table Size for a Trace Table
titleSuffix: SQL Server Profiler
description: Find out how to limit the size of a trace table. Use SQL Server Profiler to specify the maximum number of rows the table can have.
author: markingmyname
ms.author: maghan
ms.date: 03/01/2017
ms.service: sql
ms.subservice: profiler
ms.topic: conceptual
---

# Set a Maximum Table Size for a Trace Table (SQL Server Profiler)

 [!INCLUDE [SQL Server Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdbmi.md)]

This topic describes how to set a maximum table size for trace tables by using [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### To set a maximum table size for a trace table  
  
1.  On the **File** menu, click **New Trace**, and then connect to an instance of SQL Server.  
  
     The **Trace Properties**dialog box appears.  
  
    > [!NOTE]  
    >  If **Start tracing immediately after making connection**is selected, the **Trace Properties**dialog box fails to appear and the trace begins instead. To turn off this setting, on the **Tools**menu, click **Options**, and clear the **Start tracing immediately after making connection** check box.  
  
2.  In the **Trace name** box, type a name for the trace.  
  
3.  In the **Template name**list, select a trace template.  
  
4.  Select the **Save to table**check box.  
  
5.  Connect to the server on which you want the trace to be stored.  
  
     The **Destination Table** dialog box appears.  
  
6.  Select a database for the trace from the **Database** list.  
  
7.  In the **Table** box, type or select a table name.  
  
8.  Select the **Set maximum rows** check box, and specify a maximum number of rows for the trace table.  
  
    > [!NOTE]  
    >  When the number of rows in the table exceeds the maximum that you have specified, the trace events are no longer recorded. However, tracing continues.  
  
## See Also  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
