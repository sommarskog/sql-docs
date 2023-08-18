---
title: "MSSQLSERVER_905"
description: "MSSQLSERVER_905"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "905 (Database Engine error)"
---
# MSSQLSERVER_905
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|905|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|DBSTARTUP_EE_PARTITIONING|  
|Message Text|Database '%.*ls' cannot be started in this edition of SQL Server because it contains a partition function '%.\*ls'. Only Enterprise edition of SQL Server supports partitioning.|  
  
## Explanation  
The database contains one or more partitioned tables or indexes. This edition of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cannot use partitioning. Therefore, the database cannot be started correctly. Partitioned tables and indexes are not available in every edition of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of features that are supported by the editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see [Features Supported by the Editions of SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## User Action  
Detach the database by using the sp_detach_db stored procedure. Move the files if it is needed, and then attach the database to an instance of a supported [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edition by using the CREATE DATABASE with the FOR ATTACH or FOR ATTACH_REBUILD_LOG option. Disable partitioning on all tables and remove the partitioning functions. Detach the database again, and reattach the database to the current server.  
  
