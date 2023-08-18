---
title: "snapshots.fn_trace_getdata (Transact-SQL)"
description: "snapshots.fn_trace_getdata (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "snapshots.fn_trace_getdata"
helpviewer_keywords:
  - "snapshots.fn_trace_getdata function"
dev_langs:
  - "TSQL"
---
# snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  This function returns all the events captured for the specified trace.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## Arguments  
 *trace_info_id*  
 The unique identifier for the primary key in the snapshots.trace_info table in the management data warehouse database. *trace_info_id* is **int**.  
  
 *start_time*  
 The time that the trace started. *start_time* is **datetime**.  
  
 *end_time*  
 The time that the trace ended. *end_time* is **datetime**.  
  
## Table Returned  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|The trace data from the snapshots.trace_data table in the management data warehouse database.<br /><br /> A list of the columns for the specified trace can be obtained by using the following query:<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **Note:** The columns that are returned by the snapshots.fn_trace_gettable function correspond to the values in the name column in the sys.trace_columns system view. The only difference is that the GroupID column is not returned by the function.|  
  
## Permissions  
 Requires SELECT permission for mdw_reader.  
  
## See Also  
 [Data Collection](../../relational-databases/data-collection/data-collection.md)  
  
  
