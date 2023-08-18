---
title: "MSSQLSERVER_8651"
description: "MSSQLSERVER_8651"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "8651 (Database Engine error)"
---
# MSSQLSERVER_8651
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|8651|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|MEMGRANT_ERR|  
|Message Text|Could not perform the requested operation because the minimum query memory is not available. Decrease the configured value for the 'min memory per query' server configuration option.|  
  
## Explanation  
Other processes are consuming server memory (exerting memory pressure in the server).  
  
## User Action  
Either decrease the configured value for the min memory per query' server configuration option or reduce the query load to the server.  
  
The following list outlines general steps that will help in troubleshooting memory errors:  
  
1.  Verify whether other applications or services are consuming memory on this server. Reconfigure less critical applications or services to consume less memory.  
  
2.  Start collecting performance monitor counters for **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**.  
  
3.  Check the following [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory configuration parameters:  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    Notice unusual settings. Correct them as necessary. Default settings are listed in "Setting Server Configuration Options" in SQL Server Books Online.  
  
4.  Check the workload (for example, number of concurrent sessions, currently executing queries).  

The following actions may make more memory available to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   If applications besides [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] are consuming resources, try stopping running these applications or consider running them on a separate server. This will remove external memory pressure.  
  
-   If you have configured **max server memory,** increase its setting.  
  
Run the following DBCC commands to free several [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory caches.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
If the problem continues, you will need to investigate further and possibly reduce workload.  
  
## See Also  
[DBCC FREESYSTEMCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[Server Configuration Options &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md)  
[SQL Server, Buffer Manager Object](~/relational-databases/performance-monitor/sql-server-buffer-manager-object.md)  
[SQL Server, Memory Manager Object](~/relational-databases/performance-monitor/sql-server-memory-manager-object.md)  
  
