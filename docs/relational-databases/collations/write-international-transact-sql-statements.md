---
title: "Write International Transact-SQL Statements"
description: "Write International Transact-SQL Statements"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "04/24/2019"
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "writing international statements"
  - "Transact-SQL international considerations"
  - "international considerations [SQL Server], Transact-SQL"
  - "Database Engine international considerations [SQL Server], Transact-SQL"
  - "statements [SQL Server], international"
  - "database international considerations [SQL Server], Transact-SQL"
  - "dates [SQL Server], international considerations"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Write International Transact-SQL Statements
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Databases and database applications that use [!INCLUDE[tsql](../../includes/tsql-md.md)] statements will become more portable from one language to another, or will support multiple languages, if the following guidelines are followed:  

-   Starting with [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)] and in [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], use either:
    -   The **char**, **varchar**, and **varchar(max)** data types with a [UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8) enabled collation, and data is encoded using UTF-8.
    -   The **nchar**, **nvarchar**, and **nvarchar(max)** data types with [supplementary character (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) enabled collation, and data is encoded using UTF-16. Using a non-SC collation results in data being encoded using UCS-2.      

    This avoids code page conversion issues. For other considerations, see [Storage differences between UTF-8 and UTF-16](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).  

-   Up to [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], replace all uses of the **char**, **varchar**, and **varchar(max)** data types with **nchar**, **nvarchar**, and **nvarchar(max)**. If using a [supplementary character (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) enabled collation, data is encoded using UTF-16. Using a non-SC collation results in data being encoded using UCS-2. This avoids code page conversion issues. For more information, see [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md). 

    > [!IMPORTANT]
    > The **text** data type is deprecated and should not be used in new development work. Plan to convert **text** data to **varchar(max)**.
  
-   When doing month and day-of-week comparisons and operations, use the numeric date parts instead of the name strings. Different language settings return different names for the months and weekdays. For example, `DATENAME(MONTH,GETDATE())` returns `May` when the language is set to U.S. English, returns `Mai` when the language is set to German, and returns `mai` when the language is set to French. Instead, use a function such as [DATEPART](../../t-sql/functions/datepart-transact-sql.md) that uses the number of the month instead of the name. Use the DATEPART names when you build result sets to be displayed to a user, because the date names are frequently more meaningful than a numeric representation. However, don't code any logic that depends on the displayed names being from a specific language.  
  
-   When you specify dates in comparisons or for input to INSERT or UPDATE statements, use constants that are interpreted the same way for all language settings:  
  
    -   ADO, OLE DB, and ODBC applications should use the ODBC timestamp, date, and time escape clauses of:  
  
         **{ ts'** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [**.**_fff_] **'}** such as: **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _yyyy_ **-** _mm_ **-** _dd_ **'}** such as: **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** such as: **{ t'10:02:20'}**  
  
    -   Applications that use other APIs, or [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts, stored procedures, and triggers, should use the unseparated numeric strings. For example, *yyyymmdd* as 19980924.  
  
    -   Applications that use other APIs, or [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts, stored procedures, and triggers should use the [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) statement with an explicit style parameter for all conversions between the **time**, **date**, **smalldate**, **datetime**, **datetime2**, and **datetimeoffset** data types and character string data types. For example, the following statement is interpreted in the same way for all language or date format connection settings:  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2022.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## See also
[CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)      
