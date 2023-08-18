---
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.reviewer: jopilov
ms.date: 03/01/2023
ms.service: sql
ms.topic: include
---
The [SQL Server Native Client](../relational-databases/native-client/sql-server-native-client.md) (often abbreviated SNAC) has been removed from [!INCLUDE[sssql22-md](sssql22-md.md)] and [!INCLUDE[ssManStudioFull](ssmanstudiofull-md.md)] 19 (SSMS). The SQL Server Native Client (SQLNCLI or SQLNCLI11) and the legacy Microsoft OLE DB Provider for SQL Server (SQLOLEDB) are not recommended for new application development. Switch to the new [Microsoft OLE DB Driver (MSOLEDBSQL) for SQL Server](../connect/oledb/oledb-driver-for-sql-server.md) or the latest [Microsoft ODBC Driver for SQL Server](../connect/odbc/microsoft-odbc-driver-for-sql-server.md) going forward. For SQLNCLI that ships as a component of [!INCLUDE [ssdenoversion-md](ssdenoversion-md.md)] (versions 2012 through 2019), see this [Support Lifecycle exception](../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md#support-lifecycle-exception).