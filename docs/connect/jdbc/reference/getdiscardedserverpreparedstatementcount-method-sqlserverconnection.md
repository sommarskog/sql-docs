---
title: "getDiscardedServerPreparedStatementCount Method (SQLServerConnection)"
description: "getDiscardedServerPreparedStatementCount Method (SQLServerConnection)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerConnection.getDiscardedServerPreparedStatementCount"
apitype: "Assembly"
---
# getDiscardedServerPreparedStatementCount Method (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Returns the number of currently outstanding prepared statement unprepare actions.

## Syntax  
  
```  
  
public int getDiscardedServerPreparedStatementCount()  
```  

## Return Value
 An **int** that contains the number of currently outstanding prepared statement unprepare actions.

## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## Remarks  
 This method is available from JDBC driver version 6.4 and onward.
 
## See Also  
 [SQLServerConnection Members](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection Class](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
