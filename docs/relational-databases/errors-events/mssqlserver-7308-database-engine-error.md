---
title: "MSSQLSERVER_7308"
description: "MSSQLSERVER_7308"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "7308 (Database Engine error)"
  - "single-threaded apartment mode"
---
# MSSQLSERVER_7308
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|7308|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|RMT_STA_DISABLED|  
|Message Text|OLE DB provider '%ls' cannot be used for distributed queries because the provider is configured to run in single-threaded apartment mode.|  
  
## Explanation  
You have used an OLE DB provider that is configured to run in single-threaded apartment (STA) mode. OLE DB providers that run in single-threaded apartment (STA) mode cannot be used for distributed queries.  
  
## User Action  
To resolve this error, configure the provider to run in multithreaded apartment (MTA) mode. If the provider does not support MTA, and the provider cannot be upgraded to a version that supports MTA, consider configuring the provider to run out-of-process. The provider vendor should be able to tell you if the provider supports MTA or running out-of-process.  
  
