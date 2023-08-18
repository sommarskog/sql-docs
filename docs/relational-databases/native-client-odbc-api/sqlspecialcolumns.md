---
title: "SQLSpecialColumns"
description: "SQLSpecialColumns"
author: markingmyname
ms.author: maghan
ms.date: "03/17/2017"
ms.service: sql
ms.subservice: native-client
ms.topic: "reference"
helpviewer_keywords:
  - "SQLSpecialColumns function"
apitype: "DLLExport"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# SQLSpecialColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  When requesting row identifiers (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** returns an empty result set (no data rows) for any requested scope other than SQL_SCOPE_CURROW. The generated result set indicates that the columns are only valid within this scope.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] does not support pseudocolumns for identifiers. The **SQLSpecialColumns** result set will identify all columns as SQL_PC_NOT_PSEUDO.  
  
 **SQLSpecialColumns** can be executed on a static cursor. An attempt to execute **SQLSpecialColumns** on an updatable (keyset-driven or dynamic) returns SQL_SUCCESS_WITH_INFO indicating the cursor type has been changed.  
  
## SQLSpecialColumns Support for Enhanced Date and Time Features  
 For information about the values returned for the columns DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH, and DECIMAL_DIGTS for date/time types, see [Catalog Metadata](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 For more general information, see [Date and Time Improvements &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## SQLSpecialColumns Support for Large CLR UDTs  
 **SQLSpecialColumns** supports large CLR user-defined types (UDTs). For more information, see [Large CLR User-Defined Types &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## See Also  
 [SQLSpecialColumns Function](../../odbc/reference/syntax/sqlspecialcolumns-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
