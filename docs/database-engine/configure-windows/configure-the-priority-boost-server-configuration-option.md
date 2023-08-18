---
title: Configure the priority boost (server configuration option)
description: Learn about the deprecated priority boost option. See how to use it to set the priority base for SQL Server in the Windows 2008 or Windows Server 2008 R2 scheduler.
author: rwestMSFT
ms.author: randolphwest
ms.date: 01/23/2023
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "priority boost option"
---
# Configure the priority boost (server configuration option)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

This article describes how to configure the **priority boost** configuration option in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[tsql](../../includes/tsql-md.md)].

> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]

Use the **priority boost** option to specify whether [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] should run at a higher scheduling priority than other processes on the same computer. If you set this option to 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] runs at a priority base of 13 in the Windows scheduler. The default is 0, which is a priority base of 7.

## Limitations and restrictions

Raising the priority too high may drain resources from essential operating system and network functions, resulting in problems shutting down SQL Server or using other operating system tasks on the server. This setting does not make the SQL Server process run at the highest operating system priority.

You do not need to use **priority boost** for performance tuning. If you do use **priority boost**, it can interfere with smooth server functioning under certain conditions, and you should only use it under exceptional circumstances. For example, Microsoft Product Support Services might use **priority boost** when they investigate a performance issue.

> [!IMPORTANT]  
Don't use **priority boost** in a SQL Server failover cluster.

## Permissions

Execute permissions on `sp_configure` with no parameters or with only the first parameter are granted to all users by default. To execute `sp_configure` with both parameters to change a configuration option or to run the `RECONFIGURE` statement, a user must be granted the ALTER SETTINGS server-level permission. The ALTER SETTINGS permission is implicitly held by the **sysadmin** and **serveradmin** fixed server roles.

## Remarks

The server must be restarted before the setting can take effect.

## Use Transact-SQL

This example shows how to use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) to enable advanced options, and then set the value of the `priority boost` option to `1`.

```sql
USE [master];
GO
EXEC sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
EXEC sp_configure 'priority boost', 1;
GO
RECONFIGURE;
GO
```

## See also

- [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)
- [Server Configuration Options (SQL Server)](server-configuration-options-sql-server.md)
- [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
