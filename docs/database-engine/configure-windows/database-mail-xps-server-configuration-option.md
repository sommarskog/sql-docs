---
title: "Database Mail XPs (server configuration option)"
description: "Learn about the DatabaseMail XPs option. View different ways of turning on this option so that you can use Database Mail in SQL Server."
author: rwestMSFT
ms.author: randolphwest
ms.date: "11/27/2018"
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "Database Mail XPs option"
  - "Database Mail [SQL Server], enabling"
---
# Database Mail XPs (server configuration option)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use the **DatabaseMail XPs** option to enable Database Mail on this server. The possible values are:  
  
- `0`: Database Mail isn't available (default).  
  
- `1`: Database Mail is available.  
  
 The setting takes effect immediately without a server stop and restart.  
  
 After enabling Database Mail, you must configure a Database Mail host database to use Database Mail.  
  
 Configuring Database Mail using the **Database Mail Configuration Wizard** enables the Database Mail extended stored procedures in the `msdb` database. If you use the **Database Mail Configuration Wizard**, you do not have to use the `sp_configure` example below.  
  
 Setting the **Database Mail XPs** option to `0` prevents Database Mail from starting. If it is running when the option is set to `0`, it continues to run and send mail until it is idle for the time configured in the `DatabaseMailExeMinimumLifeTime` option.  
  
## Examples
 The following example enables the Database Mail extended stored procedures.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  

The following example enables the Database Mail extended stored procedures if it is not already enabled.

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## See Also
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
