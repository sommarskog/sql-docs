---
title: "storesLowerCaseQuotedIdentifiers Method"
description: "storesLowerCaseQuotedIdentifiers Method (SQLServerDatabaseMetaData)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerDatabaseMetaData.storesLowerCaseQuotedIdentifiers"
apitype: "Assembly"
---
# storesLowerCaseQuotedIdentifiers Method (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retrieves whether this database treats mixed-case SQL identifiers that are enclosed in quotation marks as case-insensitive and stores them in lowercase.  
  
## Syntax  
  
```  
  
public boolean storesLowerCaseQuotedIdentifiers()  
```  
  
## Return Value  
 **true** if the identifiers are stored in lowercase. Otherwise, **false**.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This storesLowerCaseQuotedIdentifiers method is specified by the storesLowerCaseQuotedIdentifiers method in the java.sql.DatabaseMetaData interface.  
  
## See Also  
 [SQLServerDatabaseMetaData Methods](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData Members](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData Class](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
