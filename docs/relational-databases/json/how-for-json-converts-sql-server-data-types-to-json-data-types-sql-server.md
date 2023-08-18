---
title: "How FOR JSON converts SQL Server data types to JSON data types"
description: "How FOR JSON converts SQL Server data types to JSON data types (SQL Server)"
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.date: 06/03/2020
ms.service: sql
ms.topic: conceptual
helpviewer_keywords:
  - "FOR JSON, data type conversion"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# How FOR JSON converts SQL Server data types to JSON data types (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  The **FOR JSON** clause uses the following rules to convert SQL Server data types to JSON types in the JSON output.  
  
|Category|SQL Server data type|JSON data type|  
|--------------|--------------|---------------|  
|Character & string types|char, nchar, varchar, nvarchar|string|  
|Numeric types|int, bigint, float, decimal, numeric|number|  
|Bit type|bit|Boolean (true or false)|  
|Date & time types|date, datetime, datetime2, time, datetimeoffset|string|  
|Binary types|varbinary, binary, image, timestamp, rowversion|BASE64-encoded string|  
|CLR types|geometry, geography, other CLR types|Not supported. These types return an error.<br /><br /> In the SELECT statement, use CAST or CONVERT, or use a CLR property or method, to convert the source data to a SQL Server data type that can be converted successfully to a JSON type. For example, use **STAsText()** for the geometry type, or use **ToString()** for any CLR type. The type of the JSON output value is then derived from the return type of the conversion that you apply in the SELECT statement.|  
|Other types|uniqueidentifier, money|string|  

## Learn more about JSON in SQL Server and Azure SQL Database  
  
### Microsoft videos

For a visual introduction to the built-in JSON support in SQL Server and Azure SQL Database, see the following videos:

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven-SQLServer2016/JSON-as-bridge-betwen-NoSQL-relational-worlds)
  
## See Also  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
