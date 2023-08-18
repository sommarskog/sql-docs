---
title: "Characteristics of a Result Set (ODBC)"
description: "Determining the Characteristics of a Result Set (ODBC)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: native-client
ms.topic: "reference"
helpviewer_keywords:
  - "result sets [ODBC], characteristics"
  - "SQL Server Native Client ODBC driver, result sets"
  - "ODBC applications, result sets"
  - "SQLDescribeCol function"
  - "metadata [ODBC]"
  - "SQLColAttribute function"
  - "SQLNumResultCols function"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Determining the Characteristics of a Result Set (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Metadata is data that describes other data. For example, result set metadata describes the characteristics of a result set, such as the number of columns in the result set, the data types of those columns, their names, precision, and nullability.  
  
 ODBC supplies metadata to applications through its catalog API functions. The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC driver implements many of the ODBC API catalog functions as calls to a corresponding [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] catalog procedure.  
  
 Applications require metadata for most result set operations. For example, the application uses the data type of a column to determine what kind of variable to bind to that column. It uses the byte length of a character column to determine how much space it must have to display data from that column. How an application determines the metadata for a column depends on the type of the application.  
  
 Vertical applications typically work with predefined tables and perform predefined operations on those tables. Because the result set metadata for such applications is defined before the application is even written and is controlled by the developer, it can be hard-coded into the application. For example, if an order ID column is defined as a 4-byte integer in the data source, the application can always bind a 4-byte integer to that column. When metadata is hard-coded in the application, a change to the tables used by the application generally implies a change to the application code.  
  
 In generic applications, especially applications that support ad hoc queries, the metadata of the result sets they create is typically unknown until run time.  
  
 To determine the characteristics of a result set, an application can call:  
  
-   [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) to determine how many columns a request returned.  
  
-   [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) or [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) to describe a column in the result set.  
  
 A well-designed application is written with the assumption that the result set is unknown and uses the information returned by these functions to bind the columns in the result set. An application can call these functions at any time after a statement is prepared or executed. However, for optimal performance, an application should call **SQLColAttribute**, **SQLDescribeCol**, and **SQLNumResultCols** after a statement is executed.  
  
 You can have multiple concurrent calls for metadata. The system catalog procedures underlying the ODBC catalog API implementations can be called by the ODBC driver while it is using static server cursors. This lets applications concurrently process multiple calls to ODBC catalog functions.  
  
 If an application uses a particular set of metadata more than one time, it will probably benefit from caching the information in private variables when it is first obtained. This prevents later calls to the ODBC catalog functions for the same information, which force the driver to make round trips to the server.  
  
## See Also  
 [Processing Results &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
