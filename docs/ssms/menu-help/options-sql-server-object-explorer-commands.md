---
title:  Options - SQL Server Object Explorer commands
description: Description of options within the SQL Server Object Explorer - Commands window.
author: erinstellato-ms
ms.author: erinstellato
ms.reviewer: maghan
ms.date: 05/24/2023
ms.service: sql
ms.subservice: ssms
ms.topic: ui-reference
---

# Options (SQL Server Object Explorer - Commands)

Use this page to specify options related to commands available from Object Explorer. To access this dialog box, go to **Tools > Options > SQL Server Object Explorer > Commands** from the top menu bar.

## Audit Log Viewer Options

| Option | Information | Description |
|--------|-------------|-------------|
| Value for Select Top <n\> Audit records command | 1000 | Specifies the number of returned rows from a server audit on the log viewer.  Specifying a value of zero (0) returns all rows (not recommended). |

## Azure Data Studio Options

| Option | Information | Description |
|--------|-------------|-------------|
| Full path the Azure Data Studio instance to invoke | | When specified, SSMS uses it to launch a new instance of Azure Data Studio (for example, C:\Program Files\Azure Data Studio\bin\azuredatastudio.com).  Leave blank to let SSMS use its heuristic. |

## Drag/Drop

| Option | Information | Description |
|--------|-------------|-------------|
| Prepend dragged object name with schema and period | **True** <br> **False** | Disable to not include the schema name when dragging objects from Object Explorer. |
| Surround object names with brackets when dragged | **True** <br> **False** | Disable to not surround object names with brackets when dragging objects from Object Explorer. Object names with spaces or closing square brackets are always escaped, regardless of this setting. |

## PowerShell Options

| Option | Information | Description |
|--------|-------------|-------------|
| Additional parameters to use when importing the SQL Server module | | When specified, PowerShell uses these parameters when running 'Import-Module SQLServer'.  Parameters can be used to force the import of a specific version of the module (for example, -RequiredVersion 22.0.59) |
| Execution policy to use | **AllSigned** <br> **Bypass** <br> **RemoteSigned** <br> **Restricted** <br> **Undefined** <br> **Unrestricted** | When specified, this value is passed as an argument to -ExecutionPolicy when a new PowerShell session is started.  Leave blank to use RemoteExecution. |
| Path to the PowerShell instance to invoke | | When specified, SSMS uses it to launch a new instance of PowerShell (for example, C:\Program Files\PowerShell\7\pwsh.exe).  The path can be an absolute or relative path.  Use this parameter to force using PS7.  Leave blank to use the 64-bit PS5. |
| Skip check on minimum required version of the module | **True** <br> **False** | When true, SSMS skips the validation of the minimum required version of the SQLServer module. It's recommended to leave as 'False'. |

## Rename Options

| Option | Information | Description |
|--------|-------------|-------------|
| Prompt to confirm the renaming of schema objects | **True** <br> **False** | When true, an attempt to rename a database object using Object Explorer prompts for confirmation unless using the context menu. |

## Table and View Options

| Option | Information | Description |
|--------|-------------|-------------|
| Value for Edit Top <n\> Rows command | 200 | Specifies the number of returned rows using the TOP clause for the Edit command.  Specifying a value of zero (0) returns all rows (not recommended). |
| Value for Select Top <n\> Rows command | 1000 | Specifies the number of returned rows using the TOP clause for the Select command.  Specifying a value of zero (0) returns all rows (not recommended). |

## Task Dialogs

| Option | Information | Description |
|--------|-------------|-------------|
| Remember task dialog position | **True** <br> **False** | Enable this option to remember the position of a task dialog or property sheet when it closes.  When the dialog or sheet reopens, it's restored to the remembered position. |