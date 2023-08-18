---
title: "Driver history for Microsoft SQL Server"
description: "This page describes Microsoft's historical data connection technologies for connecting to SQL Server."
author: David-Engel
ms.author: v-davidengel
ms.date: 11/03/2022
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
---
# Driver history for Microsoft SQL Server

This page describes Microsoft's historical data connection technologies for connecting to SQL Server.

## ODBC

There are three distinct generations of Microsoft ODBC drivers for SQL Server. The first "SQL Server" ODBC driver still ships as part of [Windows Data Access Components](#microsoft-or-windows-data-access-components). This driver isn't recommended for new development. Starting in SQL Server 2005, the [SQL Server Native Client](#sql-server-native-client) includes an ODBC interface and is the ODBC driver that shipped with SQL Server 2005 through SQL Server 2012. This driver also isn't recommended for new development. After SQL Server 2012, the [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) is the driver that is updated with the most recent server features going forward.

### SQL Server Native Client

SQL Server Native Client was a stand-alone library that is used for both OLE DB and ODBC. SQL Server Native Client (often abbreviated SNAC) was included in SQL Server 2005 through 2012. SQL Server Native Client can be used for applications that need to take advantage of new features introduced in SQL Server 2005 through SQL Server 2012. (Microsoft/Windows Data Access Components aren't updated for these new features in SQL Server.) For new features beyond SQL Server 2012, SQL Server Native Client won't be updated. [!INCLUDE[snac-removed-oledb-and-odbc](../includes/snac-removed-oledb-and-odbc.md)]

For complete documentation of the SQL Server Native Client, see the [SQL Server Native Client documentation](../relational-databases/native-client/sql-server-native-client-programming.md).

### Microsoft ODBC Driver for SQL Server

After SQL Server 2012, the primary ODBC driver for SQL Server has been developed and released as the Microsoft ODBC Driver for SQL Server. For more information, see the [Microsoft ODBC Driver for SQL Server documentation](./odbc/microsoft-odbc-driver-for-sql-server.md).

## OLE DB

There are three distinct generations of Microsoft OLE DB providers for SQL Server. The first "Microsoft OLE DB Provider for SQL Server" (SQLOLEDB) still ships as part of [Windows Data Access Components](#microsoft-or-windows-data-access-components). This provider won't be updated with new features and it isn't recommended to use this driver for new development. Starting in SQL Server 2005, the [SQL Server Native Client](#sql-server-native-client) includes an OLE DB provider interface (SQLNCLI) and is the OLE DB provider that shipped with SQL Server 2005 through SQL Server 2017. It was [announced as deprecated in 2011](/archive/blogs/sqlnativeclient/microsoft-is-aligning-with-odbc-for-native-relational-data-access) and it isn't recommended to use this driver for new development. In 2017, OLE DB data access technology was later [undeprecated and a new planned release was announced](/archive/blogs/sqlnativeclient/announcing-the-new-release-of-ole-db-driver-for-sql-server) for 2018. The new [Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)](../connect/oledb/oledb-driver-for-sql-server.md) is currently maintained and supported.

## ADO.NET

ADO.NET is a set of classes that defines an interface for accessing any kind of data source, both relational and non-relational. ADO.NET was introduced with the Microsoft .NET Framework and continues to be improved and maintained in .NET. The SqlClient library is an ADO.NET data provider that provides connectivity to SQL Server and Azure SQL data sources.

### System.Data.SqlClient

System.Data.SqlClient is included as part of .NET Framework and .NET Core. Up until 2019, it was receiving regular feature updates. With the announcements of the [future of .NET Core, .NET Framework](https://devblogs.microsoft.com/dotnet/net-core-is-the-future-of-net/), and [.NET in general](https://devblogs.microsoft.com/dotnet/introducing-net-5/), development of SqlClient needed to shift to a package outside of .NET. System.Data.SqlClient is still supported but isn't receiving feature updates and isn't recommended for new development.

### Microsoft.Data.SqlClient

[Introduced in 2019](https://devblogs.microsoft.com/dotnet/introducing-the-new-microsoftdatasqlclient/), the Microsoft SqlClient Data Provider for SQL Server is an ADO.NET data provider supporting applications that target .NET Framework, .NET Core, and .NET Standard. For more information about the Microsoft.Data.SqlClient namespace, see [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md).

## JDBC

### Microsoft JDBC Driver for SQL Server

Introduced in 2000, the Microsoft JDBC Driver for SQL Server continues to be improved and maintained. It was open-sourced in 2016. For the latest information, including how to download the driver, see [Overview of the JDBC Driver](./jdbc/overview-of-the-jdbc-driver.md).

## PHP

### Microsoft Drivers for PHP for SQL Server

Introduced in 2009 as an open-source project, the Microsoft Drivers for PHP for SQL Server continue to be improved and maintained. For the latest information, including how to download the PHP driver, see [Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md).

## Node.js

### Microsoft Driver for Node.js for SQL Server

The Microsoft Driver for Node.js for SQL Server allows Node.js applications on Microsoft Windows and Microsoft Azure to access Microsoft SQL Server and Microsoft Azure SQL Database. Development efforts are no longer being focused on this driver. It isn't recommended to create new applications using the Microsoft Driver for Node.js for SQL Server.

For more information about the Microsoft Driver for Node.js for SQL Server, see [WindowsAzure / node-sqlserver](https://github.com/Azure/node-sqlserver).

### Tedious

Microsoft currently contributes to and supports the open-source tedious module in Node.js for connectivity to SQL Server using JavaScript. For more information, see [Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md).

## Microsoft or Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC) are shipped with and supported by Windows for application backwards compatibility and aren't part of the current SQL Server technology stack. No new features will be added to components in MDAC/WDAC and it isn't recommended to use them for new application development.

For the purposes of this document, you can divide the MDAC/WDAC stack into the following components, based on technology and products:

* **ADO** (including ADOMD and ADOX)
* **OLE DB** (including OLE DB Core Services, SQL Server OLE DB Provider, Oracle OLE DB Provider, OLE DB Provider for ODBC Drivers, Data Shape Provider, and Remote Data Provider)
* **ODBC** (including ODBC Driver Manager, SQL ODBC Driver, and Oracle ODBC Driver)

### MDAC/WDAC components

MDAC/WDAC includes these components:

* **ODBC:** The Microsoft Open Database Connectivity (ODBC) interface is a C programming-language interface that allows applications to access data from different kinds of Database Management Systems (DBMS). Applications that use this API are limited to accessing relational data sources only.
* **OLE DB:** OLE DB is a set of COM interfaces for accessing data in different kinds of data stores. OLE DB providers exist for accessing data in databases, file systems, message stores, directory services, workflow, and document stores.
* **ADO:** ActiveX Data Objects (ADO) provides a high-level programming model. Although a little less performant than coding to OLE DB or ODBC directly, ADO is straightforward to learn and use. It can be used from script languages, such as Microsoft Visual Basic Scripting Edition (VBScript) or Microsoft JScript.
* **ADOMD:** ADO Multi-Dimensional (ADOMD) is to be used with multidimensional data providers such as Microsoft OLAP Provider, also known as Microsoft Analysis Services Provider. No major feature enhancements have been made to it since MDAC 2.0.
* **ADOX:** ADO Extensions for DDL and Security (ADOX) enable the creation and modification of definitions of a database, table, index, or stored procedure. You can use ADOX with any provider. The Microsoft Jet OLE DB Provider provides full support for ADOX, while the Microsoft SQL Server OLE DB Provider provides limited support.
* **Microsoft SQL Server Network Libraries:** The SQL Server Network Libraries allow SQLOLEDB and SQLODBC to communicate with the SQL Server database. The following SQL Server Network Libraries have been deprecated in MDAC/WDAC releases: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet, and RPC. TCP/IP and Named Pipes will continue to be supported and are available on the 64-bit Windows operating system.
* **MSDASQL:** The Microsoft OLE DB Provider for ODBC (MSDASQL) allows applications that are built on OLE DB and ADO (which uses OLEDB internally) to access data sources through an ODBC driver. MSDASQL is an OLEDB provider that connects to ODBC, instead of a database. It is meant as a bridge from OLE DB to an ODBC driver when no direct OLE DB provider exists for a data source. MSDASQL ships with the Windows operating system, and Windows Server 2008 and Vista SP1 were the first Windows releases to include a 64-bit version of the technology.

### Deprecated MDAC/WDAC Components

These components are still supported in the current release of MDAC/WDAC, but they might be removed in future releases. When developing new applications, Microsoft recommends that you avoid using these components. Additionally, when you upgrade or modify existing applications, remove any dependency on these components.

* **SQLOLEDB:** The Microsoft OLE DB Provider for SQL Server (SQLOLEDB), which supports access to Microsoft SQL Server, has been deprecated. Its connectivity to future versions of SQL Server may not be supported. The ability to connect to versions earlier than SQL Server 7 will be removed from the operating system after Windows 7. New applications should use the Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL), which supports new SQL Server features. Existing applications should migrate to the Microsoft OLE DB Driver for SQL Server as well for better performance, reliability, and supportability. For more information, see [Updating an Application to OLE DB Driver for SQL Server from MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).
* **SQLODBC:** The Microsoft SQL Server ODBC Driver (SQLODBC), which supports access to Microsoft SQL Server, has been deprecated. Its connectivity to future versions of SQL Server may not be supported. The ability to connect to versions earlier than SQL Server 7 will be removed from the operating system after Windows 7. New applications should use the Microsoft ODBC Driver for SQL Server on Windows, which supports new SQL Server features. Existing applications should migrate to the Microsoft ODBC Driver for SQL Server as well for better performance, reliability, and supportability. For relevant information, see [Updating an Application to SQL Server Native Client from MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).
* **Microsoft Jet Database Engine 4.0:** Starting with version 2.6, MDAC no longer contains Jet components. In other words, MDAC 2.6, 2.7, and 2.8 don't contain Microsoft Jet, the Microsoft Jet OLE DB Provider, the ODBC Desktop Database Drivers, or Jet Data Access Objects (DAO). 

  There's no 64-bit version of the Jet Database Engine, the Jet OLEDB Driver, the Jet ODBC Drivers, or Jet DAO available. For more information, see [KB article 957570](https://support.microsoft.com/kb/957570). On 64-bit versions of Windows, 32-bit Jet runs under the Windows WOW64 subsystem. For more information on WOW64, see the [MSDN WOW64 documentation](/windows/desktop/WinProg64/wow64-implementation-details). Native 64-bit applications cannot communicate with the 32-bit Jet drivers running in WOW64.

  Instead of Microsoft Jet, Microsoft recommends using [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) when developing new, non-Microsoft Access applications requiring a relational data store. These new or converted Jet applications can continue to use Jet with the intention of using Microsoft Office 2003 and earlier files (.mdb and .xls) for non-primary data storage. However, for these applications, you should plan to migrate from Jet to the Microsoft Access Database Engine. You can [download the Microsoft Access Database Engine](https://www.microsoft.com/download/details.aspx?id=54920), which allows you to read from and write to pre-existing files in either Office 2003 (.mdb and .xls) or the Office 2007 (*.accdb, *.xlsm, *.xlsx and *.xlsb) file formats.

  > [!IMPORTANT]
  > Please read the 2007 Office System End User License Agreement for specific usage limitations.

  > [!NOTE]
  > SQL Server applications can also access the 2007 Office System, and earlier, files from SQL Server heterogeneous data connectivity and Integrations Services capabilities as well, via the 2007 Office System Driver. Additionally, 64-bit SQL Server applications can access to 32-bit Jet and 2007 Office System files by using 32-bit SQL Server Integration Services (SSIS) on 64-bit Windows.

* **Microsoft OLE DB Provider for Data Shaping (MSDADS):** With MSDADS, you can create hierarchical relationships between keys, fields, or rowsets in an application. No major feature enhancements have been made since MDAC 2.1. This Provider has been deprecated. Microsoft recommends that you use XML, instead of MSDADS.
* **Oracle ODBC and Oracle OLE DB:** The Microsoft Oracle ODBC Driver (Oracle ODBC) and Microsoft OLE DB Provider for Oracle (Oracle OLE DB) provide access to Oracle database servers. They're built by using Oracle Call Interface (OCI) version 7 and provide full support for Oracle 7. Also, it uses Oracle 7 emulation to provide limited support for Oracle 8 databases. Oracle no longer supports applications that use OCI version 7 calls. These technologies are deprecated. If you're using Oracle data sources, you should migrate to Oracle-supplied driver and provider.
* **Remote Data Services (RDS):** RDS is a proprietary Microsoft mechanism for accessing remote ADO Recordset objects across the Internet or an Intranet. RDS is deprecated; no major feature enhancements have been made to RDS since MDAC 2.1. Microsoft has released the .NET Framework, which has extensive SOAP capabilities and replaces RDS components. All RDS server components will be removed from the operating system after Windows 7.
* **Jet Replication Objects (JRO):** JRO is deprecated. JRO is used within ADO with Jet (*.mdb) databases to create and compress Jet Databases (.mdb's) and perform Jet Replication Management. MDAC 2.7 will be its last release. JRO won't be available on the 64-bit Windows operating system. JRO isn't supported in the Microsoft Access 2007 file format (*.accdb).
* **16-bit ODBC Support:** If you're using 16-bit applications, you should migrate to a 32-bit application. 16-bit functionality is deprecated and is being removed from 64-bit operating systems. For more information, see [Knowledge base article 896458](https://support.microsoft.com/kb/896458).
* **OLEDB Simple Provider (MSDAOSP):** OLEDB Simple Provider offers a framework for quickly building OLE DB providers over simple data. MSDAOSP is deprecated.
* **ODBC Cursor Library:** ODBC Cursor Library (ODBCCR32.dll) provides limited client-side data cursors. ODBC Cursor Library has been deprecated; your application can use server-side cursor implementations as a replacement.
* **OLE DB Out-of-Process Interface Remoting:** OLEDB Interface remoting (msdaps.dll) was an attempt to allow OLE DB providers to run out of process. OLEDB Out-of-Process Interface remoting is deprecated.
* **AppleTalk and Banyan Vines SQL Network Libraries:** The Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet, and RPC SQL network libraries are deprecated. If you're using any of these technologies, you should modify your applications to use one of the other network libraries, such as TCP/IP and Named Pipe.

### MDAC/WDAC Releases

Here's a list of the supportability scenarios of past MDAC/WDAC releases, starting with the earliest.

* **MDAC 1.5, MDAC 2.0, and MDAC 2.1:** These versions of MDAC were independent releases that were released through the Microsoft Windows NT Option Pack, the Microsoft Windows Platform SDK, or the MDAC Web site. These versions of MDAC are no longer supported.
* **MDAC 2.5:** This version of MDAC was included with the Windows 2000 operating system. Service packs of MDAC 2.5 were included with corresponding Windows 2000 service packs.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1, and SP2 were included with Microsoft SQL Server 2000 RTM, SP1, and SP2, respectively. Additionally, these MDAC service packs were released to the MDAC Web site following the Microsoft SQL Server 2000 service-pack release schedule. You can install this version of MDAC and its service packs on Windows 2000, Windows Millennium Edition, Windows NT, Windows 95, and Windows 98 platforms. This version of MDAC no longer is supported.
* **MDAC 2.7:** This version of MDAC was included with the Microsoft Windows XP RTM and SP1 operating systems. You can install this version of MDAC and its service packs on Windows 2000, Windows Millennium, Windows NT, and Windows 98 platforms. You can install this version on the Windows XP platform only through the operating system or its services packs. This version of MDAC no longer is supported.
* **MDAC 2.8:** This version of MDAC was included with Windows Server 2003 and Windows XP SP2 and later. You also can install this version of MDAC and its service packs on Windows 2000.

  * The 32-bit version of MDAC 2.8 also was released to the MDAC Web site at the same time that Windows Server 2003 was released to the customer.
  * The 64-bit version of MDAC 2.8 was released with the 64-bit version of Windows Server 2003 and Windows XP.

* **Windows Data Access Components (WDAC):** MDAC changed its name to WDAC - "Windows Data Access Components" starting with Windows Vista and Windows Server 2008. WDAC is included as part of the operating system and isn't available separately for redistribution. Serviceability for WDAC is subject to the life cycle of the operating system.

  32-bit and 64-bit versions of WDAC are released with the 32-bit and 64-bit versions of the Windows operating systems, respectively.

## Obsolete data access technologies

Obsolete technologies are technologies that have not been enhanced or updated in several product releases and that will be excluded from future product releases. Don't use these technologies when you write new applications. When you modify existing applications that are written by using these technologies, consider migrating those applications to ADO.NET or another current technology.

The following components are considered obsolete:

* **DB-Library:** DB-Library is a SQL Server-specific programming model that includes C APIs. There have been no feature enhancements to the DB-Library since SQL Server 6.5. Its final release was with SQL Server 2000, and it won't be ported to the 64-bit Windows operating system.
* **Embedded SQL (E-SQL):** E-SQL is a SQL Server-specific programming model that enables Transact-SQL statements to be embedded in Visual C code. No feature enhancements have been made to the E-SQL since SQL Server 6.5. Its final release was with SQL Server 2000, and it won't be ported to the 64-bit Windows operating system.
* **Data Access Objects (DAO):** DAO provides access to JET (Access) databases. This API can be used from Microsoft Visual Basic, Microsoft Visual C++, and scripting languages. It was included with Microsoft Office 2000 and Office XP. DAO 3.6 is the final version of this technology. It won't be available on the 64-bit Windows operating system.
* **Remote Data Objects (RDO):** RDO was designed specifically to access remote ODBC relational data sources, and made it easier to use ODBC without complex application code. It was included with Microsoft Visual Basic versions 4, 5, and 6. RDO version 2.0 was the final version of this technology.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
