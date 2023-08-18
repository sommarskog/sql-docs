---
title: "MSSQLSERVER_10520"
description: "MSSQLSERVER_10520"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "10520 (Database Engine error)"
---
# MSSQLSERVER_10520
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|10520|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|PG_PARAM_NOT_ALLOWED|  
|Message Text|Cannot create plan guide '%.*ls' because @type was specified as '%ls' and a non-NULL value is specified for the parameter '%ls'. This type requires a NULL value for the parameter. Specify NULL for the parameter, or change the type to one that allows a non-NULL value for the parameter.|  
  
## Explanation  
The type specified in @type requires a NULL value for the specified parameter, however a non-NULL value was supplied.  
  
## User Action  
Specify NULL for the parameter, or change the type to one that allows a non-NULL value for the parameter.  
  
## See Also  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Plan Guides](~/relational-databases/performance/plan-guides.md)  
  
