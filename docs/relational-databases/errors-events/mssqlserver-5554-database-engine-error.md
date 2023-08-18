---
title: "MSSQLSERVER_5554"
description: "MSSQLSERVER_5554"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "5554 (Database Engine error)"
---
# MSSQLSERVER_5554
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|MSSQLSERVER|  
|Event ID|5554|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|FS_MINIVER_OVERFLOW|  
|Message Text|The total number of versions for a single file has reached the maximum limit set by the file system.|  
  
## Explanation  
In multiple active result sets (MARS) or trigger scenarios, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uses the miniversion specified by the operating system.  
  
## User Action  
Try to avoid repeated updates to the data in the same transaction.  
  
