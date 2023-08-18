---
title: "MSSQLSERVER_2530"
description: "MSSQLSERVER_2530"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
---
# MSSQLSERVER_2530
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|2530|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC_INDEX_IS_OFFLINE|  
|Message Text|The index "%.*ls" on table "%.\*ls" is disabled.|  
  
## Explanation  
The DBCC statement cannot proceed because the specified index is disabled. After an index is disabled, it remains in a disabled state until it is rebuilt or dropped and re-created.  
  
## User Action  
  
1.  Enable the disabled index by using one of the following methods:  
  
    -   ALTER INDEX statement with the REBUILD clause  
  
    -   CREATE INDEX with the DROP_EXISTING clause  
  
    -   DBCC DBREINDEX  
  
2.  Rerun the DBCC statement.  
  
## See Also  
[Enable Indexes and Constraints](~/relational-databases/indexes/enable-indexes-and-constraints.md)  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[DBCC DBREINDEX &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)  
  
