---
title: "Connect To Azure SQL Database (AccessToSQL)"
description: "Connect To Azure SQL Database (AccessToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
helpviewer_keywords:
  - "Connect to SQL Azure dialog box"
---
# Connect To Azure SQL Database (AccessToSQL)
Use the Connect to SQL Azure dialog box to connect to the database in Azure SQL Database that you want to migrate.  
  
To access this dialog box, on the **File** menu, select **Connect to SQL Azure**. If you have previously connected, the command is **Reconnect to SQL Azure.**  
  
## Options  
**Server Name**  
  
Select or enter the Server Name for connecting to SQL Azure.  
  
**Database**  
  
Select, enter or **Browse** the Database name.  
  
> [!IMPORTANT]  
> SSMA for Access does not support connection to master database in SQL Azure.  
  
**User name**  
  
Enter the user name that SSMA will use to connect to Azure SQL Database  
  
**Password**  
  
Enter the password for the user name.  
  
**Encrypt**  
  
SSMA recommends encrypted connection to SQL Azure.  
  
## Create database  
To create a new database, follow the following steps  
  
1.  click on browse button that is present in the Connect to SQL Azure dialog box  
  
2.  If there are no databases, two menu items appear  
  
    1.  **(no databases found)** which is disabled and grayed out all the time  
  
    2.  **Create new database** which is always enabled, enabling the user to create a new database. Upon clicking this menu item, create database dialog box is present with database name and size.  
  
3.  At the time of database creation, these two parameters is given as input.  
  
    1.  **Database Name:** Enter the Database name.  
  
    2.  **Database Size   :** Select the Database size that you need to create in SQL Azure account.  
  
