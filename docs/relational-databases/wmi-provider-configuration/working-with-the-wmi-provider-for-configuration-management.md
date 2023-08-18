---
title: "Use the WMI Provider for Configuration Management"
description: Learn about the WMI Provider for Configuration Management, including binding, specifying a connection string, and permissions/server authentication.
author: markingmyname
ms.author: maghan
ms.date: "04/12/2019"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "permissions [WMI]"
  - "connection strings [WMI]"
  - "security [WMI]"
  - "WMI Provider for Configuration Management, connection strings"
  - "WMI Provider for Configuration Management, security"
  - "late binding [WMI]"
  - "WMI Provider for Configuration Management, late binding"
  - "binding [WMI]"
---
# Working with the WMI Provider for Configuration Management

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

This article provides guidance about how to program with the WMI Provider for Computer Management.

## Binding  
 The WMI Provider for Configuration Management is a COM object model and it supports early and late binding. With late binding you can use script languages, such as VBScript, to manipulate the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services, network settings, and aliases programmatically.  
  
## Specifying a Connection String

Applications direct the WMI Provider for Configuration Management to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by connecting to a WMI namespace defined by the provider. The Windows WMI service maps this namespace to the provider DLL, and loads the DLL into memory. All instances of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] are represented with a single WMI namespace.

The namespace defaults to the following format. In the format, `VV` is the major version number of SQL Server. The number is discoverable by running `SELECT @@VERSION;`.

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

When you connect by using PowerShell, the leading `\\.\` must be removed. For example, the following PowerShell code lists all WMI classes for a SQL Server 2016, which is major version 13.

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

You can use following PowerShell code to query all available WMI ComputerManagement namespaces.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **Note:** If you are connecting through Windows Firewall you will need to make sure your computers are configured appropriately. See the "Connecting Through Windows Firewall" article in the Windows Management Instrumentation documentation on [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [Web site](https://go.microsoft.com/fwlink/?linkid=15426).  
  
## Permissions and Server Authentication  
 To access the WMI Provider for Configuration Management, the client WMI management script must be running in the context of an administrator on the target computer. You need to be a member of the local Windows administrators group on the computer you want to manage.  
  
 The administrator can set group policies to control user access to WMI providers. For more information about setting group policies see "Group Policy and MMC" in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager Help.  
  
 The WMI management script can be used to update the account under which [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services run.  
  
 Security certificates are supported by the WMI Provider for Configuration Management. For more information about certificates, see [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## See Also  
 [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
