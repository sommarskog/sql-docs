---
title: "MSSQLSERVER_4846"
description: "MSSQLSERVER_4846"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "4846 (Database Engine error)"
---
# MSSQLSERVER_4846
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|4846|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|BULKPROV_MEMORY|  
|Message Text|The bulk data provider failed to allocate memory.|  
  
## Explanation  
Memory allocation failed.  
  
## User Action  
Follow these general steps to troubleshoot memory errors:  
  
1.  Verify whether other applications or services are consuming memory on this server. Reconfigure less critical applications or services to consume less memory.  
  
2.  Start collecting performance monitor counters for **SQL Server: Buffer Manager**, **SQL Server: Memory Manager**.  
  
3.  Check the following SQL Server memory configuration parameters:  
  
    -   **max server memory**  
  
    -   **min server memory**  
  
    -   **min memory per query**  
  
    Notice any unusual settings. Correct them as necessary. Account for memory requirements for [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Default settings are listed in "Setting Server Configuration Options" in SQL Server Books Online.  
  
4.  Observe DBCC MEMORYSTATUS output and the way it changes when you see these error messages.  
  
5.  Check the workload (for example, number of concurrent sessions, currently executing queries).  
  
The following actions may make more memory available to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   If applications besides SQL Server are consuming resources, try stopping running these applications or consider running them on a separate server. This will remove external memory pressure.  
  
-   If you have configured **max server memory,** increase its setting.  
  
Run the following DBCC commands to free several [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory caches.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
If the problem continues, you will need to investigate further and possibly reduce workload.  
  
