---
title: "MSSQLSERVER_10519"
description: "MSSQLSERVER_10519"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "10519 (Database Engine error)"
---
# MSSQLSERVER_10519
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|10519|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|Message Text|Cannot create plan guide '%.\*ls' because the hints specified in **\@hints** cannot be applied to the statement specified by either **\@stmt** or **\@statement_start_offset**. Verify that the hints can be applied to the statement.|  
  
## Explanation  
The hints specified in **\@hints** cannot be applied to the statement specified by either **\@stmt** or **\@statement_start_offset**.  
  
## User Action  
Specify hints that can be applied to the statement.  
  
## See Also  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
