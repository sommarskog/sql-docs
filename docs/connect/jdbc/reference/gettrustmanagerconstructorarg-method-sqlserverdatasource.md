---
title: "getTrustManagerConstructorArg Method (SQLServerDataSource)"
description: "getTrustManagerConstructorArg Method (SQLServerDataSource)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerDataSource.getTrustManagerConstructorArg"
apitype: "Assembly"
---
# getTrustManagerConstructorArg Method (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Returns the String value of the TrustManagerConstructorArg connection property.
  
## Syntax  
  
```  
  
public java.lang.String getTrustManagerConstructorArg()  
```  
  
## Return Value  
 A **String** that contains the value of the TrustManagerConstructorArg connection property, or null if no value is set.  
  
## Remarks  
 If the TrustManagerClass property is not set, the [getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md) method returns null.  
  
## See Also  
 [SQLServerDataSource Members](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource Class](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
