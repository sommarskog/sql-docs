---
title: "MSSQLSERVER_41332"
description: "MSSQLSERVER_41332"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "41332 (Database Engine error)"
---
# MSSQLSERVER_41332
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Event ID|41332|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|SQL_SNAPSHOT_NOT_SUPPORTED|  
|Message Text|Memory optimized tables and natively compiled stored procedures cannot be accessed or created when the session TRANSACTION ISOLATION LEVEL is set to SNAPSHOT.|  
  
## Explanation  
The transaction was started in snapshot isolation level and then attempted to use an incompatible feature.  
  
## User Action  
Start the transaction with a different isolation level. For more information, see [In-Memory OLTP &#40;In-Memory Optimization&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## See Also  
[In-Memory OLTP &#40;In-Memory Optimization&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
