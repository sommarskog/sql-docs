---
title: "supportsMultipleOpenResults Method (SQLServerDatabaseMetaData)"
description: "supportsMultipleOpenResults Method (SQLServerDatabaseMetaData)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerDatabaseMetaData.supportsMultipleOpenResults"
apitype: "Assembly"
---
# supportsMultipleOpenResults Method (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retrieves whether it is possible to have multiple [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objects returned from a [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) object simultaneously.  
  
## Syntax  
  
```  
  
public boolean supportsMultipleOpenResults()  
```  
  
## Return Value  
 **true** if supported. Otherwise, **false**.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This supportsMultipleOpenResults method is specified by the supportsMultipleOpenResults method in the java.sql.DatabaseMetaData interface.  
  
## See Also  
 [SQLServerDatabaseMetaData Methods](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData Members](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData Class](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
