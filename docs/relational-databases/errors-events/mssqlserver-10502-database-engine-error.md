---
title: "MSSQLSERVER_10502"
description: "MSSQLSERVER_10502"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "10502 (Database Engine error)"
---
# MSSQLSERVER_10502
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|10502|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|PG_DUP_FOUND|  
|Message Text|Cannot create plan guide '%.*ls' because the statement specified by @stmt and @module_or_batch, or by @plan_handle and @statement_start_offset, matches the existing plan guide '%.\*ls' in the database. Drop the existing plan guide before creating the new plan guide.|  
  
## Explanation  
A plan guide exists for the specified statement.  
  
## User Action  
Drop the existing plan guide before creating the new plan guide.  
  
## See Also  
[Plan Guides](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
