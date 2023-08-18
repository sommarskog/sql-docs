---
title: "MSSQLSERVER_41307"
description: "MSSQLSERVER_41307"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "41307 (Database Engine error)"
---
# MSSQLSERVER_41307
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Event ID|41307|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|HK_HEKATON_ROW_LIMIT|  
|Message Text|The row size limit of *number* bytes for memory optimized tables has been exceeded. Please simplify the table definition.|  
  
## Explanation  
The row size limit for memory optimized tables is 8,060 bytes. For more information, see [Table and Row Size in Memory-Optimized Tables](~/relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md). For more information, see [In-Memory OLTP &#40;In-Memory Optimization&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## See Also  
[In-Memory OLTP &#40;In-Memory Optimization&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
