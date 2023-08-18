---
title: "MSSQLSERVER_2527"
description: "MSSQLSERVER_2527"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "2527 (Database Engine error)"
---
# MSSQLSERVER_2527
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|2527|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBCC_INDEX_FILEGROUP_IS_OFFLINE|  
|Message Text|Unable to process index I_NAME of table O_NAME because filegroup F_NAME is offline.|  
  
## Explanation  
This informational message indicates that the index cannot be checked because one of the filegroups that stores data for the index is offline. The state of the files in a filegroup determines the availability of the whole filegroup. For a filegroup to be available, all files within the filegroup must be online. If there are no other problems, all other indexes of the same object will be checked.  
  
## User Action  
To view the state of the files for the specified filegroup, query either the **sys.database_files** or **sys.master_files** catalog view.  
  
Restore the offline file from a backup.  
  
## See Also  
[sys.database_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[sys.master_files &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
