---
title: "MSSQLSERVER_15599"
description: "MSSQLSERVER_15599"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "15599 (Database Engine error)"
---
# MSSQLSERVER_15599
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|15599|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Message Text|Auditing and permissions can't be set on local temporary objects.|  
  
## Explanation  
Auditing and permissions do not have any effect when set for local or global temp objects. The statements do not result in an error (the operations will return success), but have no effect.  
  
This behavior has not changed, however beginning with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], this informational message alerts the user.  
  
## User Action  
No action is necessary, but consider removing statements that attempt to set auditing or permissions on local or global temp objects.  
  
