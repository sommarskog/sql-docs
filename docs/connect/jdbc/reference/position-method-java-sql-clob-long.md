---
title: "position Method (java.sql.Clob, long)"
description: "position Method (java.sql.Clob, long)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerClob.position (java.sql.Clob, long)"
apitype: "Assembly"
---
# position Method (java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Returns the character position of the specified CLOB object in the CLOB based on the given starting position.  
  
## Syntax  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### Parameters  
 *searchstr*  
  
 The substring to search for.  
  
 *start*  
  
 The position at which to begin searching. The first position is 1.  
  
## Return Value  
 The position at which the substring appears, or -1 if it is not present. The first position is 1.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This position method is specified by the position method in the java.sql.Clob interface.  
  
## See Also  
 [position Method &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob Methods](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob Members](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob Class](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
