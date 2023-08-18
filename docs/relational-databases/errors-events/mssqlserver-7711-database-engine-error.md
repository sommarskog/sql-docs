---
title: "MSSQLSERVER_7711"
description: "MSSQLSERVER_7711"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "7711 (Database Engine error)"
---
# MSSQLSERVER_7711
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|7711|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|PRT_RANGE_OVERLAP|  
|Message Text|The DATA_COMPRESSION option was specified more than once for the table or index or one of its partitions.|  
  
## Explanation  
An error occurred in the DATA_COMPRESSION option in one of the following statements:  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
If the table or index cited is partitioned, the DATA_COMPRESSION option was listed more than one time for at least one of the partitions. If the table or index is not partitioned, the DATA_COMPRESSION option was cited more than one time.  
  
## User Action  
For a partitioned table or index, make sure that the DATA_COMPRESSION option is specified only one time for each partition. For a table or index that is not partitioned, use the DATA_COMPRESSION option only one time in the statement.  
  
