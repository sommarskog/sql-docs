---
title: "MSSQLSERVER_617"
description: "MSSQLSERVER_617"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "617 (Database Engine error)"
---
# MSSQLSERVER_617
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|617|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|NODESHASH|  
|Message Text|Descriptor for object ID %ld in database ID %d not found in the hash table during attempt to unhash it. A work table is missing an entry. Rerun the query. If a cursor is involved, close and reopen the cursor.|  
  
## Explanation  
SQL Server cannot locate the work table for a specific entry.  
  
## User Action  
  
1.  If a cursor is involved, close the cursor and re-open the cursor.  
  
2.  Run the query again.  
  
