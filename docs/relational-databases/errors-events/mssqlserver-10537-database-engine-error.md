---
title: "MSSQLSERVER_10537"
description: "MSSQLSERVER_10537"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "10537 (Database Engine error)"
---
# MSSQLSERVER_10537
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|10537|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|PG_DUP_ENABLED|  
|Message Text|Cannot enable plan guide '%.*ls' because the enabled plan guide '%.\*ls' contains the same scope and starting offset value as the statement. Disable the existing plan guide before enabling the specified plan guide.|  
  
## Explanation  
An existing plan guide contains the same scope and starting offset value as the statement in the specified plan guide.  
  
## User Action  
Disable the existing plan guide before enabling the specified plan guide.  
  
## See Also  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
