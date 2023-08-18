---
title: "Create a Table for Storing FILESTREAM Data"
description: Learn how to create a table for storing FILESTREAM data in SQL Server. See which columns and attributes to use in the Transact-SQL code.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: filestream
ms.topic: conceptual
helpviewer_keywords:
  - "FILESTREAM [SQL Server], table storage"
---
# Create a Table for Storing FILESTREAM Data
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic shows how to create a table for storing FILESTREAM data.  
  
 When the database has a FILESTREAM filegroup, you can create or modify tables to store FILESTREAM data. To specify that a column contains FILESTREAM data, you create a **varbinary(max)** column and add the FILESTREAM attribute.  
  
### To create a table to store FILESTREAM data  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], click **New Query** to display the Query Editor.  
  
2.  Copy the [!INCLUDE[tsql](../../includes/tsql-md.md)] code from the following example into the Query Editor. This [!INCLUDE[tsql](../../includes/tsql-md.md)] code creates a FILESTREAM-enabled table called Records.  
  
3.  To create the table, click **Execute**.  
  
## Example  
 The following code example shows how to create a table that is named `Records`. The `Id` column is a `ROWGUIDCOL` column and is required to use FILESTREAM data with Win32 APIs. The `SerialNumber` column is a `UNIQUE INTEGER`. The `Chart` column is a `FILESTREAM` column and is used to store the `Chart` in the file system.  
  
> [!NOTE]  
>  This example refers to the Archive database that is created in [Create a FILESTREAM-Enabled Database](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## See Also  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
