---
title: "MSSQLSERVER_3437"
description: "MSSQLSERVER_3437"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "3437 (Database Engine error)"
---
# MSSQLSERVER_3437
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|3437|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|NODTC|  
|Message Text|An error occurred while recovering database '%.*ls'. Unable to connect to Microsoft Distributed Transaction Coordinator (MS DTC) to check the completion status of transaction %S_XID. Fix MS DTC, and run recovery again.|  
  
## Explanation  
One or more distributed transactions that were using [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator (MS DTC) were incomplete when the database was shut down. Recovery of this database failed because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cannot connect to MS DTC to complete or roll back the transactions.  
  
## User Action  
To recover this database, you must first resolve the problem with MS DTC. To investigate the problem with MS DTC, examine the Windows event logs. If you cannot resolve the problem with MS DTC and recover the database, restore a backup of database.  
  
