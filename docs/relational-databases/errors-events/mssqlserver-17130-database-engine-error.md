---
title: "MSSQLSERVER_17130"
description: "MSSQLSERVER_17130"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "17130 (Database Engine error)"
---
# MSSQLSERVER_17130
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|17130|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|INIT_NOLOCKSPACE|  
|Message Text|Not enough memory for the configured number of locks. Attempting to start with a smaller lock hash table, which may impact performance. Contact the database administrator to configure more memory for this instance of the Database Engine.|  
  
## Explanation  
Not enough memory for the desired lock manager hash table size.  An attempt will be made to allocate a smaller hash table.  
  
## User Action  
Check server memory configuration parameters (min/max server memory), check for memory pressures. Provide SQL Server more memory.  
  
