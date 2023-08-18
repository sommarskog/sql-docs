---
title: "Configure the remote data archive (server configuration option)"
description: Learn how to use the remote data archive option in SQL Server to specify whether databases and tables on the server can be enabled for Stretch.
author: rwestMSFT
ms.author: randolphwest
ms.date: 07/25/2022
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
---
# Configure the remote data archive (server configuration option)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use the **remote data archive** option to specify whether databases and tables on the server can be enabled for Stretch. For more info, see [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).

> [!IMPORTANT]  
> Stretch Database is deprecated in [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)]. [!INCLUDE [ssNoteDepFutureAvoid-md](../../includes/ssnotedepfutureavoid-md.md)]

The **remote data archive** option can have the following values.

|Value|Description|  
|-----------|-----------------|  
|0|Databases and tables on the server cannot be enabled for Stretch.|  
|1|Databases and tables on the server can be enabled for Stretch.|

Running **sp_configure** to set the value of the **remote data archive** option requires sysadmin or serveradmin permissions.

## Example

The following example first displays the current setting of the **remote data archive** option. Then the example enables the **remote data archive** option by setting its value to 1.

```sql
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```

To disable the option, set the value to 0.

## See also

- [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)
- [Stretch Database](../../sql-server/stretch-database/stretch-database.md)
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)
