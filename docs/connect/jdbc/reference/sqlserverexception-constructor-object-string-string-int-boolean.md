---
title: "SQLServerException Constructor (java.lang.Object, java.lang.String, java.lang.String, int, boolean)"
description: "SQLServerException Constructor (java.lang.Object, java.lang.String, java.lang.String, int, boolean)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apitype: "Assembly"
---
# SQLServerException Constructor (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Initializes a new instance of the [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) class when given an **object**, a **string** object, a **string** object, an **int**, and a **boolean**.

## Syntax  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

			
```  
  
#### Parameters  
 *obj*  
  
 The IO buffer that generated the exception.

 *errText*  
  
 A string containing the error text.
  
 *sqlState*  
  
 An enum object that contains the SQL state.
 
 *errNum*  
  
 An int that contain the error code for the exception.
 
 *bStack*  
  
 A boolean that indicates if the stack trace should be generated.
  
## See Also  
 [SQLServerException Constructors](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException Members](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException Class](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
