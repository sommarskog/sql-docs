---
title: "MSSQLSERVER_5245"
description: "MSSQLSERVER_5245"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "5245 (Database Engine error)"
---
# MSSQLSERVER_5245
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|5245|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Message Text|Object ID O_ID (object 'NAME'): DBCC could not obtain a lock on this object because the lock request time-out period was exceeded. This object has been skipped and will not be processed.|  
  
## Explanation  
A lock time-out occurred while DBCC was waiting on a table lock for the specified object.  
  
## User Action  
Rerun the DBCC command.  
  
