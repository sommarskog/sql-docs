---
title: "Migrating Access Data into SQL Server - Azure SQL Database (AccessToSQL)"
description: "Migrating Access Data into SQL Server - Azure SQL Database (AccessToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
ms.custom: intro-migration
helpviewer_keywords:
  - "bulk loading data"
  - "data, loading into SQL Azure"
  - "data, loading into SQL Server"
  - "migrating databases, loading data"
  - "migrating databases, options"
  - "options, migrating data"
  - "SQL Azure, migrating data into"
  - "SQL Server, migrating data into"
---
# Migrating Access Data into SQL Server - Azure SQL Database (AccessToSQL)
After you have successfully created the database objects into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], you can migrate data from Access to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure.  
  
## Setting Migration Options  
Before you migrate data into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure, review the project migration options in the **Project Settings** dialog box. In this dialog box, you can set the migration batch size, table locking, constraint checking, insertion trigger firing, identity and null value handling, and how to handle dates that are out of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] range. For more information, see [Project Settings (Migration)](./project-settings-migration-accesstosql.md).  
  
## Migrating Data  
Migrating data is a bulk-load operation that moves rows of data into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure in transactions. The number of rows to be loaded into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure in each transaction is configured in the project settings.  
  
To view migration messages, make sure the Output pane is visible. If it is not, on the **View** menu, select **Output**.  
  
**To migrate data**  
  
1.  Make sure you have loaded the Access database objects into [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure.  
  
2.  In Access Metadata Explorer, select the objects that contain the data that you want to migrate:  
  
    -   To migrate data for an entire database, select the check box next to the database name.  
  
    -   To migrate data from individual tables, expand the database, expand **Tables**, and then select the check box next to the table. To omit data from individual tables, clear the check box.  
  
3.  Right-click **Databases** and then select **Migrate Data**.  
  
You also can migrate data outside of SSMA by using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** command-line utility or [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. For more information about these tools, see [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.  
  
## Next Step  
If you have Access database applications that you want to continue to use after migration, link the Access database tables to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or SQL Azure tables. For more information, see [Linking Access Applications to SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## See Also  
[Migrating Access Databases to SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Setting Conversion and Migration Options](setting-conversion-and-migration-options-accesstosql.md)  
