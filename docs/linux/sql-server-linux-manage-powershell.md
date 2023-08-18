---
title: Manage SQL Server on Linux with PowerShell
description: Learn details about SQL Server PowerShell and see a couple of examples on how to use Windows with SQL Server on Linux.
author: rwestMSFT
ms.author: randolphwest
ms.date: 12/16/2021
ms.service: sql
ms.subservice: linux
ms.topic: conceptual
---
# Use PowerShell on Windows to manage SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

This article introduces [SQL Server PowerShell](../powershell/sql-server-powershell.md) and walks you through a couple of examples on how to use it with SQL Server on Linux. PowerShell support for SQL Server is currently available on Windows, macOS, & Linux. This article walks you through using a Windows machine to connect to a remote SQL Server instance on Linux.

## Install the newest version of SQL PowerShell on Windows

[SQL PowerShell](../powershell/download-sql-server-ps-module.md) on Windows is maintained in the PowerShell Gallery. When working with SQL Server, you should always use the most recent version of the SqlServer PowerShell module.

## Before you begin

Read the [Known Issues](sql-server-linux-release-notes-2017.md#known-issues) for SQL Server on Linux.

## Launch PowerShell and import the *sqlserver* module

Let's start by launching PowerShell on Windows. Use <kbd>Win</kbd>+<kbd>R</kbd>, on your Windows computer, and type **PowerShell** to launch a new Windows PowerShell session.

SQL Server provides a PowerShell module named **SqlServer**. You can use the **SqlServer** module to import the SQL Server components (SQL Server provider and cmdlets) into a PowerShell environment or script.

Copy and paste the following command at the PowerShell prompt to import the **SqlServer** module into your current PowerShell session:

```powershell
Import-Module SqlServer
```

Type the following command at the PowerShell prompt to verify that the **SqlServer** module was imported correctly:

```powershell
Get-Module -Name SqlServer
```

PowerShell should display information similar to the following output:

```
ModuleType Version    Name          ExportedCommands
---------- -------    ----          ----------------
Script     21.1.18102 SqlServer     {Add-SqlAvailabilityDatabase, Add-SqlAvailabilityGroupList...
```

## Connect to SQL Server and get server information

Let's use PowerShell on Windows to connect to your SQL Server instance on Linux and display a couple of server properties.

Copy and paste the following commands at the PowerShell prompt. When you run these commands, PowerShell will:

- Display a dialog that prompts you for the hostname or IP address of your instance
- Display the *Windows PowerShell credential request* dialog, which prompts you for the credentials. You can use your *SQL username* and *SQL password* to connect to your SQL Server instance on Linux
- Use the **Get-SqlInstance** cmdlet to connect to the **Server** and display a few properties

Optionally, you can just replace the `$serverInstance` variable with the IP address or the hostname of your SQL Server instance.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Connect to the Server and get a few properties
Get-SqlInstance -ServerInstance $serverInstance -Credential $credential
# done
```

PowerShell should display information similar to the following output:

```output
Instance Name                   Version    ProductLevel UpdateLevel  HostPlatform HostDistribution                
-------------                   -------    ------------ -----------  ------------ ----------------                
your_server_instance            14.0.3048  RTM          CU13         Linux        Ubuntu 
```

> [!NOTE]
> If nothing is displayed for these values, the connection to the target SQL Server instance most likely failed. Make sure that you can use the same connection information to connect from SQL Server Management Studio. Then review the [connection troubleshooting recommendations](sql-server-linux-troubleshooting-guide.md#connection).

## Using the SQL Server PowerShell Provider

Another option for connecting to your SQL Server instance is to use the [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  This provider allows you to navigate SQL Server instance similar to as if you were navigating the tree structure in Object Explorer, but at the cmdline. By default, this provider is presented as a PSDrive named `SQLSERVER:\`, which you can use to connect and navigate SQL Server instances that your domain account has access to. For more information on how to set up Active Directory authentication for SQL Server on Linux, see [Configuration steps](./sql-server-linux-active-directory-auth-overview.md#configuration-steps).

You can also use SQL authentication with the SQL Server PowerShell Provider. To do this, use the `New-PSDrive` cmdlet to create a new PSDrive and supply the proper credentials in order to connect.

In this example below, you'll see one example of how to create a new PSDrive using SQL authentication.

```powershell
# NOTE: We are reusing the values saved in the $credential variable from the above example.
New-PSDrive -Name SQLonDocker -PSProvider SqlServer -Root 'SQLSERVER:\SQL\localhost,10002\Default\' -Credential $credential
```

You can confirm that the drive was created by running the `Get-PSDrive` cmdlet.

```powershell
Get-PSDrive
```

Once you've created your new PSDrive, you can start navigating it.

```powershell
dir SQLonDocker:\Databases
```

Here's what the output might look like. You might notice the output is similar to what [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) will display at the Databases node. It displays the user databases, but not the system databases.

```powershell
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2022   Normal      209.63 MB    1.31 MB Simple       130 sa
AdventureWorksDW2022 Normal      167.00 MB   32.47 MB Simple       110 sa
AdventureWorksDW2022 Normal      188.00 MB   78.10 MB Simple       120 sa
AdventureWorksDW2022 Normal      172.00 MB   74.76 MB Simple       130 sa
AdventureWorksDW2022 Normal      208.00 MB   40.57 MB Simple       140 sa
```

If you need to see all databases on your instance, one option is to use the [Get-SqlDatabase](/powershell/module/sqlserver/Get-SqlDatabase) cmdlet.

## Examine SQL Server error logs

The following steps use PowerShell on Windows to examine error logs connect on your SQL Server instance on Linux. We'll also use the **Out-GridView** cmdlet to show information from the error logs in a grid view display.

Copy and paste the following commands at the PowerShell prompt. They might take a few minutes to run. These commands do the following:
- Display a dialog that prompts you for the hostname or IP address of your instance
- Display the *Windows PowerShell credential request* dialog, which prompts you for the credentials. You can use your *SQL username* and *SQL password* to connect to your SQL Server instance on Linux
- Use the **Get-SqlErrorLog** cmdlet to connect to the SQL Server instance on Linux and retrieve error logs since **Yesterday**
- Pipe the output to the **Out-GridView** cmdlet

Optionally, you can replace the `$serverInstance` variable with the IP address or the hostname of your SQL Server instance.

```powershell
# Prompt for instance & credentials to login into SQL Server
$serverInstance = Read-Host "Enter the name of your instance"
$credential = Get-Credential

# Retrieve error logs since yesterday
Get-SqlErrorLog -ServerInstance $serverInstance -Credential $credential -Since Yesterday | Out-GridView
# done
```

## See also
- [SQL Server PowerShell](../powershell/sql-server-powershell.md)
- [SqlServer cmdlets](/powershell/module/sqlserver)
