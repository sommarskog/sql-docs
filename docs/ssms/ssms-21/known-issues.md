---
title: Known issues in SQL Server Management Studio
description: Learn about known issues in SQL Server Management Studio (SSMS).
author: erinstellato-ms
ms.author: erinstellato
ms.reviewer: randolphwest, maghan
ms.date: 12/18/2024
ms.service: sql
ms.subservice: ssms
ms.topic: troubleshooting-general
---

# Known issues in SQL Server Management Studio 21 Preview

[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

This page lists known issues for [!INCLUDE [ssms-21-md](../includes/ssms-21-md.md)].

| Feature | Details | Workaround |
| --- | --- | --- |
| Analysis Services | There's currently no support for Analysis Services in [!INCLUDE [ssms-21-md](../includes/ssms-21-md.md)]. | Use SSMS 20.2 to connect to Analysis Services, we'll bring back Analysis Services in a future preview. |
| Arm64 | There's no support for Arm64, and SSMS can't be installed on Arm64 devices. | Run SSMS on a device that isn't Arm64. |
| Database Diagrams | Closing a new database diagram before saving generates the error "Object reference not set to an instance of an object. (SqlEditors)". | Save the new database diagram before closing the editor in Database Diagrams. |
| Designers | Closing the view editor before saving in the View Designer generates the error "Object reference not set to an instance of an object. (SqlEditors)". | Save the new view before closing the editor in the View Designer. |
| Find | The **Quick Find** option is not available. Typically accessed through **Edit** > **Find and Replace** > **Quick Find**, or with **CTRL + F**, the full **Find and Replace** appears instead. | There's currently no workaround in SSMS 21 Preview. |
| Integration Services | There's currently no support for Integration Services in [!INCLUDE [ssms-21-md](../includes/ssms-21-md.md)]. | Use SSMS 20.2 to connect to Integration Services, we'll bring back Integration Services in a future preview. |
| License | The "Microsoft Software License Terms" link in the Visual Studio Install splash screen doesn't access a valid URL. | Access the license for SSMS 21 from the "license" link within the Visual Studio Installer, available when customizing the SSMS 21 installation. |
| Maintenance Plans | There's currently no support for creating or editing maintenance plans in [!INCLUDE [ssms-21-md](../includes/ssms-21-md.md)]. | Use SSMS 20.2 to create or edit maintenance plans, we'll bring back Integration Services in a future preview. |
| Menu | Opening a folder from **File** > **Recent Projects and Solutions** generates one of the following errors: "System.InvalidOperationException: Can't enque project dependencies calculation before starting solution load" or "An exception of type NullReferenceException has been encountered." if opening the folder also opens one or more files that were open in the editor when the folder was last closed. | Closing the error allows work to continue. Alternatively, close all files in the editor before closing a folder. |
| Menu | The **File** > **Add** > **New Project or Existing Project** menu option isn't available. | Use SSMS 20.2 to create a new project or open an existing one. |
| Menu | The **File** > **File** menu option isn't available. | Use **File** > **New Query with current connection** or the New Query button to open a new query editor. |
| Menu | The **File** > **Open** > **Project/Solution** menu option isn't available. | Use SSMS 20.2 to open an existing project or solution. |
| Options | Enabling Per Monitor Awareness (PMA) by checking **Optimize rendering for screens with different pixel densities (requires restart)** within **Tools** > **Options** can cause issues with dialogs not rendering. | Don't enable **Optimize rendering for screens with different pixel densities (requires restart)** within **Tools** > **Options**. |
| Version | The version of SSMS listed in the Visual Studio Installer for Preview 2.1 doesn't match the version listed in **Help** > **About**. | There is no workaround and this will be resolved in a future preview. |

## Related content

- [Install SQL Server Management Studio 21 Preview](../install/install.md)
