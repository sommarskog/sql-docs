---
title: "MSSQLSERVER_5231"
description: "MSSQLSERVER_5231"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "5231 (Database Engine error)"
---
# MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|5231|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|Message Text|Object ID O_ID (object 'NAME'): A deadlock occurred while trying to lock this object for checking. This object has been skipped and will not be processed.|  
  
## Explanation  
A deadlock occurred when DBCC was trying to lock the object, and DBCC was chosen as the deadlock victim. The object will not be processed.  
  
## User Action  
None  
  
