---
title: Change server authentication mode
description: Learn how to change the server authentication mode in SQL Server. You can use either SQL Server Management Studio or Transact-SQL for this task.
author: rwestMSFT
ms.author: randolphwest
ms.date: 03/30/2023
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "sa account"
  - "authentication [SQL Server], changing modes"
  - "server authentication mode [SQL Server]"
  - "modifying server authentication mode"
---
# Change server authentication mode

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

This article describes how to change the server authentication mode in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)]. During installation, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] is set to either **Windows Authentication mode** or **SQL Server and Windows Authentication mode**. After installation, you can change the authentication mode at any time.

If **Windows Authentication mode** is selected during installation, the `sa` login is disabled and a password is assigned by setup. If you later change authentication mode to **SQL Server and Windows Authentication mode**, the `sa` login remains disabled. To use the `sa` login, use the ALTER LOGIN statement to enable the `sa` login and assign a new password. The `sa` login can only connect to the server by using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.

## Before you begin

The `sa` account is a well known [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account and it is often targeted by malicious users. Don't enable the `sa` account unless your application requires it. It's important that you use a strong password for the `sa` login.

## <a id="change-authentication-mode-with-ssms"></a> Change authentication mode with SQL Server Management Studio

1. In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) Object Explorer, right-click the server, and then select **Properties**.

1. On the **Security** page, under **Server authentication**, select the new server authentication mode, and then select **OK**.

1. In the [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dialog box, select **OK** to acknowledge the requirement to restart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

1. In Object Explorer, right-click your server, and then select **Restart**. If [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent is running, it must also be restarted.

## Enable `sa` login

You can enable the `sa` login with SSMS or Transact-SQL.

### Use SSMS

1. In Object Explorer, expand **Security**, expand Logins, right-click **sa**, and then select **Properties**.

1. On the **General** page, you might have to create and confirm a password for the `sa` login.

1. On the **Status** page, in the **Login** section, select **Enabled**, and then select **OK**.

### Use Transact-SQL

The following example enables the `sa` login and sets a new password. Replace `<enterStrongPasswordHere>` with a strong password before you run it.

```sql
ALTER LOGIN sa ENABLE;
GO
ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>';
GO
```

## Change authentication mode (Transact-SQL)

The following example changes Server Authentication from mixed mode (Windows and SQL) to Windows only.

> [!CAUTION]
> The following example uses an extended stored procedure to modify the server registry. Serious problems might occur if you modify the registry incorrectly. These problems might require you to reinstall the operating system. Microsoft cannot guarantee that these problems can be resolved. Modify the registry at your own risk.

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE',
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1;
GO
```

> [!NOTE]  
> The permissions required to change the authentication mode are [sysadmin](../../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles) or [Control Server](../../relational-databases/security/permissions-database-engine.md)

## See also

- [Strong Passwords](../../relational-databases/security/strong-passwords.md)
- [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)
- [ALTER LOGIN (Transact-SQL)](../../t-sql/statements/alter-login-transact-sql.md)
- [Connect to SQL Server When System Administrators Are Locked Out](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)
