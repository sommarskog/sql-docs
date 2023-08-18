---
title: SqlErrorLogFile class
description: Provides properties for viewing information about a SQL Server log file.
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 02/23/2023
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
---
# SqlErrorLogFile class

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Provides properties for viewing information about a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log file.

## Syntax

```csharp
class SQLErrorLogFile
{
    uint32ArchiveNumber;
    stringInstanceName;
    datetimeLastModified;
    uint32LogFileSize;
    stringName;
};
```

## Properties

The SQLErrorLogFile class defines the following properties.

| Property | Description |
| --- | --- |
| ArchiveNumber | Data type: **uint32**<br /><br />Access type: Read-only<br /><br />The archive number for the log file. |
| InstanceName | Data type: **string**<br /><br />Access type: Read-only<br /><br />Qualifiers: Key<br /><br />The name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] where the log file resides. |
| LastModified | Data type: **datetime**<br /><br />Access type: Read-only<br /><br />The date that the log file was last modified. |
| LogFileSize | Data type: **uint32**<br /><br />Access type: Read-only<br /><br />The log file size, in bytes. |
| Name | Data type: **string**<br /><br />Access type: Read-only<br /><br />Qualifiers: Key<br /><br />The name of the log file. |

## Remarks

| Type | Name |
| --- | --- |
| MOF | - `sqlmgmprovider.mof` ([!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later versions)<br />- `sqlmgmproviderxpsp2up.mof` ([!INCLUDE [sssql19-md](../../includes/sssql19-md.md)] and earlier versions) |
| DLL | `sqlmgmprovider.dll` |
| Namespace | `\root\Microsoft\SqlServer\ComputerManagement10` |

## Example

The following example retrieves information about all [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log files on a specified instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. To run the example, replace \<*Instance_Name*> with the name of the instance, for example, 'Instance1'.

```vbnet
on error resume next
set strComputer = "."
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")
  
For Each logFile in LogFiles
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _
    & "Log File Name:  " & logFile.Name & vbNewLine _
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _
    & "Last Modified:  " & logFile.LastModified & vbNewLine _
  
Next
```

## Comments

When *InstanceName* isn't provided in the WQL statement, the query returns information for the default instance. For example, the following WQL statement returns information about all log files from the default instance (MSSQLSERVER).

```wql
"SELECT * FROM SqlErrorLogFile"
```

## Security

To connect to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log file through WMI, you must have the following permissions on both the local and remote computers:

- Read access to the **Root\Microsoft\SqlServer\ComputerManagement10** WMI namespace. By default, everyone has read access through the Enable Account permission.

  > [!NOTE]  
  > For information about how to verify WMI permissions, see the Security section of the topic [View Offline Log Files](../../relational-databases/logs/view-offline-log-files.md).

- Read permission to the folder that contains the error logs. By default the error logs are located in the following path (where \<*Drive>* represents the drive where you installed [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] and \<*InstanceName*> is the name of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):

  **\<Drive>:\Program Files\Microsoft SQL Server\MSSQL11** **.\<InstanceName>\MSSQL\Log**

If you're connecting through a firewall, ensure that an exception is set in the firewall for WMI on remote target computers. For more information, see [Connecting to WMI Remotely Starting with Windows Vista](/windows/win32/wmisdk/connecting-to-wmi-remotely-starting-with-vista).

## See also

- [SqlErrorLogEvent Class](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md)
- [View Offline Log Files](../../relational-databases/logs/view-offline-log-files.md)
