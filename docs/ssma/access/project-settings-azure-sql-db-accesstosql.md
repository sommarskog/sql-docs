---
title: "Project Settings (Azure SQL Database) (AccessToSQL)"
description: "Project Settings (Azure SQL Database) (AccessToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
f1_keywords:
  - "ssma.access.projectsettingssqlazure.f1"
helpviewer_keywords:
  - "Project Settings dialog box, SQL Azure"
  - "SQL Azure settings"
---
# Project Settings (Azure SQL Database) (AccessToSQL)
The SQL Azure project settings let you configure the Azure SQL Database suffix to be added in the connection dialog and also allow implementing heartbeat mechanism in SQL Azure connection.  
  
The SQL Azure pane is available in the **Project Settings** and **Default Project Settings** dialog boxes.  
  
-   Use the Project Settings dialog box to set configuration options for the current project. To access the SQL Azure settings, on the **Tools** menu, select **Project Settings**, click **General** at the bottom of the left pane, and then select **SQL Azure**.  
  
-   Use the Default Project Settings dialog box to set configuration options for all projects. To access the SQL Azure settings, on the **Tools** menu, select **DefaultProject Settings**, select the project type as "SQL Azure" in **Migration Target Version** combo box to access the settings in SQL Azure pane, click **General** at the bottom of the left pane, and then select **SQL Azure**.  
  
## Options  
  
## Connectivity  
**Heartbeat Interval**  
  
Specifies a time interval to be used for heartbeat mechanism to keep the SQL Azure connection alive in 'minutes : seconds' format.  
  
**Default Value**:'4:45'  
  
The value should be specified in 'm:ss' format (for example, '4:45' or '0:50').  
  
**SQL Azure Server Suffix**  
  
Specifies the SQL Azure server suffix  
  
**Default Value**: 'database.windows.net'.  
  
