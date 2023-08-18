---
title: "MSSQLSERVER_3151"
description: "MSSQLSERVER_3151"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "3151 (Database Engine error)"
---
# MSSQLSERVER_3151
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|3151|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|LDDB_MASTER_LOAD_FAILED|  
|Message Text|Failed to restore master database. Shutting down SQL Server. Check the error logs, and rebuild the master database. For more information about how to rebuild the master database, see SQL Server Books Online.|  
  
## Explanation  
This is a general error message indicating various problems with the **master** database.  
  
## User Action  
Check the error logs for more information. To create a usable **master** database, run Setup.exe with the REBUILDDATABASE option. For more information see "How to: Install SQL Server from the Command Prompt" in SQL Server Books Online.  
  
