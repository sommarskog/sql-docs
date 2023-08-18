---
title: "MSSQLSERVER_7901"
description: "MSSQLSERVER_7901"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "7901 (Database Engine error)"
---
# MSSQLSERVER_7901
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|7901|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Message Text|The repair statement was not processed. This level of repair is not supported when the database is in emergency mode.|  
  
## Explanation  
The database is in emergency mode and a repair level other than REPAIR_ALLOW_DATA_LOSS has been specified. Repairs cannot be made in emergency mode unless REPAIR_ALLOW_DATA_LOSS is specified.  
  
## User Action  
Rerun the command and specify the REPAIR_ALLOW_DATA_LOSS option.  
  
