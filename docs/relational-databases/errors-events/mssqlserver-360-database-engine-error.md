---
title: "MSSQLSERVER_360"
description: "MSSQLSERVER_360"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "360 (Database Engine error)"
---
# MSSQLSERVER_360
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|360|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DML_UPDATE_SPARSE_AND_COLSET|  
|Message Text|The target column list of an INSERT, UPDATE, or MERGE statement cannot contain both a sparse column and the column set that contains the sparse column. Rewrite the statement to include either the sparse column or the column set, but not both.|  
  
## Explanation  
A column set is an untyped XML representation that combines some columns of a table into a structured output. An attempt was made to modify both the column set and a column that is included in the column set, causing two references to the same column.  
  
## User Action  
Rewrite the statement to include references to either the column or the column set, but do not include both in the statement.  
  
