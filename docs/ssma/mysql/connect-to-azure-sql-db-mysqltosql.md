---
title: "Connect to Azure SQL Database (MySQLToSQL)"
description: "Connect to Azure SQL Database (MySQLToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
---
# Connect to Azure SQL Database (MySQLToSQL)
Use the Connect to SQL Azure dialog box to connect to the database in Azure SQL Database that you want to migrate.  
  
To access this dialog box, on the **File** menu, select **Connect to SQL Azure**. If you have previously connected, the command is **Reconnect to SQL Azure.**  
  
## Options  
**Server Name**  
  
Select or enter the Server Name for connecting to SQL Azure.  
  
**Database**  
  
Select, enter or **Browse** the Database name.  
  
> [!IMPORTANT]  
> SSMA for MySQL does not support connection to master database in SQL Azure.  
  
**User name**  
  
Enter the user name that SSMA will use to connect to Azure SQL Database  
  
**Password**  
  
Enter the password for the user name.  
  
**Encrypt**  
  
SSMA recommends encrypted connection to SQL Azure.  
  
## Create Azure Database  
If there are no databases in the SQL Azure account, you can create the very first database.  
  
To create a new database for the very first time, follow the following steps  
  
1.  Click on Browse button that is present in the Connect to SQL Azure dialog box  
  
2.  If there are no databases, the following two menu items appear.  
  
    1.  **(no databases found)** which is disabled and grayed out all the time  
  
    2.  **Create new database** which is enabled only when there are no databases on SQL Azure account. Upon clicking this menu item, Create Azure Database dialog box is present with database name and size.  
  
3.  At the time of database creation, the following two parameters are given as input:  
  
    1.  **Database Name:** Enter the Database name.  
  
    2.  **Database Size:** Select the Database size that you need to create in SQL Azure account.  
  
