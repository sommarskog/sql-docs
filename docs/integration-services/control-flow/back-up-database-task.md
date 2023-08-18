---
title: "Back Up Database Task"
description: "Back Up Database Task"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.designer.backupdatabasetask.f1"
helpviewer_keywords:
  - "database backups [Integration Services]"
  - "Back Up Database task [Integration Services]"
  - "backing up databases [Integration Services]"
  - "transaction log backups [Integration Services]"
  - "backing up transaction logs [Integration Services]"
---
# Back Up Database Task

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  The Back Up Database task performs different types of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database backups. For more information, see [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
 By using the Back Up Database task, a package can back up a single database or multiple databases. If the task backs up only a single database, you can choose the backup component: the database, or its files and filegroups.  
  
## Supported Recover Models and Backup Types  
 The following table lists the recovery models and backup types that the Back Up Database task supports.  
  
|Recovery model|Database|Database differential|Transaction log|File or file differential|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Required|Optional|Not supported|Not supported|  
|Full|Required|Optional|Required|Optional|  
|Bulk-logged|Required|Optional|Required|Optional|  
  
 The Back Up Database task encapsulates a Transact-SQL BACKUP statement. For more information, see [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md).  
  
## Configuration of the Back Up Database Task  
 You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. This task is in the **Maintenance Plan Tasks** section of the **Toolbox** in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer.  
  
 For more information about the properties that you can set in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:  
  
-   [Back Up Database Task &#40;Maintenance Plan&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 For more information about how to set these properties in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:  
  
-   [Set the Properties of a Task or Container](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
