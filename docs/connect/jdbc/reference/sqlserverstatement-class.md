---
title: "SQLServerStatement Class"
description: "SQLServerStatement Class"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# SQLServerStatement Class
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Represents the basic implementation of JDBC statement functionality.  
  
 **Package:** com.microsoft.sqlserver.jdbc  
  
 **Implements:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## Syntax  
  
```  
  
public class SQLServerStatement  
```  
  
## Remarks  
 The SQLServerStatement class also provides a number of base class implementation methods for the JDBC prepared statement and callable statements. The basic role of the SQLServerStatement class is to run SQL statements, and then return update counts and result sets to the user application.  
  
 This class supports unwrapping to SQLServerStatement class, the ISQLServerStatement interface, and the java.sql.Statement interface. For more information, see [Wrappers and Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## See Also  
 [SQLServerStatement Members](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [JDBC Driver API Reference](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
