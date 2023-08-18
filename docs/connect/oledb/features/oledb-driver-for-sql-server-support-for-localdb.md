---
title: OLE DB Driver for SQL Server Support for LocalDB
description: Learn how to connect to a lightweight version of SQL Server, called LocalDB, using OLE DB Driver for SQL Server.
author: David-Engel
ms.author: v-davidengel
ms.date: 04/20/2021
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
---
# OLE DB Driver for SQL Server Support for LocalDB

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Beginning in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], a lightweight version of SQL Server, called LocalDB, will be available. This article discusses how to connect to a database in a LocalDB instance.

## Remarks

For more information about LocalDB, including how to install LocalDB and configure your LocalDB instance, see:

- [SQL Server Express LocalDB Reference](../../../relational-databases/sql-server-express-localdb-reference.md)
- [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-express-localdb.md)

LocalDB allows you to:

- Use `sqllocaldb.exe i` to discover the name of the default instance.

- Use the `AttachDBFilename` connection string keyword to specify which database file the server should attach. When using `AttachDBFilename`, if you don't specify the name of the database with the `Database` connection string keyword, the database will be removed from the LocalDB instance when the application closes.

- Specify a LocalDB instance in your connection string:

```cpp
SERVER=(localdb)\v11.0
```

 If necessary, you can create a LocalDB instance with sqllocaldb.exe. You can also use sqlcmd.exe to add and modify databases in a LocalDB instance. For example, `sqlcmd -S (localdb)\v11.0`.

## See Also

[OLE DB Driver for SQL Server Features](oledb-driver-for-sql-server-features.md)
