---
title: "MSSQLSERVER_41399"
description: "MSSQLSERVER_41399"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "41399 (Database Engine error)"
---
# MSSQLSERVER_41399
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Event ID|41399|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|MAX_SORT_ROW_WIDTH_EXCEEDED|  
|Message Text|The sort operation is too complex. Consult SQL Server Books Online for more information.|  
  
## Explanation  
Sorting the result of join and aggregation operations increases the complexity of the sort operation by increasing the size of the row in the sort buffer. This error means that the size of the row is larger than the maximum size supported by the sort operator in natively compiled stored procedures. Note that the size of a row in the sort buffer is determined solely by the number of joins and the number and type of aggregate functions. The size of the rows in the base tables does not affect the size of the row in the buffer.  
  
## User Action  
Decrease the complexity of the query by removing joins or aggregate functions.  
  
## See Also  
[In-Memory OLTP &#40;In-Memory Optimization&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
