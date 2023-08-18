---
title: "Getting Started with SSMA for MySQL Console (MySQLToSQL)"
description: "Getting Started with SSMA for MySQL Console (MySQLToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
ms.custom: intro-get-started
helpviewer_keywords:
  - "MySQL Console, launching console"
  - "MySQL Console, output conventions"
---
# Getting Started with SSMA for MySQL Console (MySQLToSQL)
This section describes the procedure to launch and get started with the MySQL console application. Also listed, herein, are the conventions used in a typical SSMA Console output window.  
  
## Launching SSMA Console  
Use the following steps to start the SSMA console application:  
  
1.  Go to **Start** and point to **All Programs**.  
  
2.  Click the **SQL Server Migration Assistant for MySQL Command Prompt** shortcut.  
  
    It displays the SSMA Console usage menu and `(/? Help)`, to help you get started with the console application.  
  
## Procedure for Using the SSMA Console  
After the console is successfully launched on your Windows system, you could use the following steps to work on it:  
  
1.  Configure SSMA Console through the script files. For more information on this section, see [Creating Script Files &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md) .  
  
2.  [Creating Variable Value Files &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [Creating the Server Connection Files &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [Executing the SSMA Console &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) based on your project needs  
  
Additional features:  
  
1.  [Securing Password](managing-passwords-mysqltosql.md) and export/ import it onto other Window machines  
  
2.  [Generate Reports](generating-reports-mysqltosql.md) to view the detailed xml output reports for assessment /conversion and data migration. Detailed error reports can also be generated for refresh and synchronization commands.  
  
## SSMA Console Output Conventions  
Upon executing the SSMA script commands and options, the console program displays the results and messages (information, error, etc.) to the user on the console or if required, redirects to an xml output file. Each type of message in the output is signified by a unique color. For example, the text message in white color denotes script file commands; the one in green color represents a prompt for user-input, and so on.  
  
![Screenshot showing an example of SSMA Console MySQL output.](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
Color-interpretation of the console output in the following table:  
  
|Color|Description|  
|---------|---------------|  
|Red|Fatal error during execution|  
|Gray|Date and Time stamp, message to the user|  
|White|Script file commands, message type|  
|Yellow|Warning|  
|Green|Prompt for user-input|  
|Cyan|Start, Finish and Result of an operation|  
  
## See Also  
[Installing SSMA for MySQL](installing-ssma-for-mysql-mysqltosql.md)  
  
