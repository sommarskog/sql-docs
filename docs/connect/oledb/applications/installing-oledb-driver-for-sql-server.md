---
title: Installing OLE DB Driver for SQL Server
description: Installing and uninstalling OLE DB Driver for SQL Server. To install the OLE DB Driver for SQL Server, you need the msoledbsql.msi installer.
author: David-Engel
ms.author: v-davidengel
ms.date: 03/30/2022
ms.service: sql
ms.subservice: connectivity
ms.topic: "reference"
ms.custom: intro-installation
helpviewer_keywords:
  - "OLE DB Driver for SQL Server, uninstalling"
  - "MSOLEDBSQL, installing"
  - "MSOLEDBSQL, uninstalling"
  - "Setup [OLE DB Driver for SQL Server]"
  - "uninstalling OLE DB Driver for SQL Server"
  - "data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server"
  - "installing OLE DB Driver for SQL Server"
  - "OLE DB Driver for SQL Server, installing"
  - "data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server"
  - "removing OLE DB Driver for SQL Server"
---
# Installing OLE DB Driver for SQL Server

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

To install the OLE DB Driver for SQL Server, you need the msoledbsql.msi installer.
Run the installer and make your preferred selections. The OLE DB Driver for SQL Server can be installed side-by-side with earlier versions of Microsoft OLE DB providers.

The files for OLE DB Driver for SQL Server (msoledbsql19.dll/msoledbsql.dll, msoledbsqlr19.dll/msoledbsqlr.rll) are installed in `%SYSTEMROOT%\system32\` . Additionally, the x64 msoledbsql.msi installs 32-bit binaries in `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]
> All appropriate registry settings for the OLE DB Driver for SQL Server are made as part of the installation process.

The header and library files for OLE DB Driver for SQL Server (msoledbsql.h and msoledbsql.lib/msoledbsql19.lib) are installed in `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\<major_version><minor_version>\SDK`. Additionally, the x64 msoledbsql.msi installs the same files in `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\<major_version><minor_version>\SDK`.

You can distribute OLE DB Driver for SQL Server through msoledbsql.msi. You might have to install OLE DB Driver for SQL Server when you deploy an application. One way to install multiple packages in what seems to the user to be a single installation is to use chainer and bootstrapper technology. For more information, see [Authoring a Custom Bootstrapper Package for Visual Studio 2005](/previous-versions/aa730839(v=vs.80)) and [Adding Custom Prerequisites](/visualstudio/deployment/creating-bootstrapper-packages).

The x64 msoledbsql.msi also installs the 32-bit version of OLE DB Driver for SQL Server. If your application targets a platform other than the one it was developed on, you can download versions of msoledbsql.msi for x64 and x86.

When you invoke msoledbsql.msi, only the client components are installed by default. The client components are files that support running an application that was developed using OLE DB Driver for SQL Server. To also install the SDK components, specify `ADDLOCAL=All` on the command line. For example:

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`

## Silent install

If you use the /passive, /qn, /qb, or /qr option with msiexec, you must also specify IACCEPTMSOLEDBSQLLICENSETERMS=YES, to explicitly indicate that you accept the terms of the end user license. This option must be specified in all capital letters.

## Installing OLE DB Driver for SQL Server as a dependency

It's important not to uninstall OLE DB Driver for SQL Server until all dependent applications are uninstalled. To provide users with a warning that your application depends on OLE DB Driver for SQL Server, use the APPGUID install option in your MSI, as follows:

`msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`

The value passed to APPGUID is your specific product code. A product code must be created when using Microsoft Installer to bundle your application setup program.
The APPGUID option requires running the installer from an elevated Command Prompt.

## See also

[Building applications with OLE DB Driver for SQL Server](building-applications-with-oledb-driver-for-sql-server.md)
