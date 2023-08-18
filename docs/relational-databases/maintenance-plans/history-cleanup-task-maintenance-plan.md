---
title: "History Cleanup Task (Maintenance Plan)"
description: Learn how to discard backup/restore history, SQL Server Agent Job history, and maintenance plan history from the msdb database using the History Cleanup Task.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 03/27/2023
ms.service: sql
ms.subservice: supportability
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.maint.historycleanup.f1"
helpviewer_keywords:
  - "History Cleanup Task dialog box"
---
# History Cleanup Task (Maintenance Plan)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use the **History Cleanup Task** dialog to discard old historical information from tables in the `msdb` database. This task supports deleting backup and restore history, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Job history, and maintenance plan history.

This statement uses the `sp_purge_jobhistory` and `sp_delete_backuphistory` statements.

## UI element list

- **Connection**

  Select the server connection to use when performing this task.

- **New**

  Create a new server connection to use when performing this task. The **New Connection** dialog box is described later in this article.

- **Backup and restore history**

  Retaining records of when recent backups were created can help [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] create a recovery plan when you want to restore a database. The retention period should be at least the frequency of full database back ups.

- **SQL Server Agent Job history**

  This history can help you troubleshoot failed jobs, or determine why database actions occurred.

- **Maintenance plan history**

  This history can help you troubleshoot failed maintenance plan jobs, or determine why database actions occurred.

- **Remove historical data older than**

  Specify age of items that you want to delete.

- **View T-SQL**

  View the [!INCLUDE[tsql](../../includes/tsql-md.md)] statements performed against the server for this task, based on the selected options.

  > [!NOTE]  
  > When the number of objects affected is large, this display can take a considerable amount of time.

## New Connection dialog box

- **Connection name**

  Enter a name for the new connection.

- **Select or enter a server name**

  Select a server to connect to when performing this task.

- **Refresh**

  Refresh the list of available servers.

- **Enter information to log on to the server**

  Specify how to authenticate against the server.

- **Use Windows integrated security**

  Connect to an instance of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] with [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Authentication.

- **Use a specific user name and password**

  Connect to an instance of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication. This option isn't available.

- **User name**

  Provide a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login to use when authenticating. This option isn't available.

- **Password**

  Provide a password to use when authenticating. This option isn't available.

## See also

- [sp_purge_jobhistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)
- [sp_delete_backuphistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)
