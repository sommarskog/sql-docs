---
title: "setStatementPoolingCacheSize Method (SQLServerDataSource)"
description: "setStatementPoolingCacheSize Method (SQLServerDataSource)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# setStatementPoolingCacheSize Method (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sets the size of the prepared statement cache for this connection. Works if disableStatementPooling is set to false and value > 0.
  
## Syntax  
  
```

public void setStatementPoolingCacheSize(boolean statementPoolingCacheSize);  
```  
  
#### Parameters  
 *statementPoolingCacheSize*  
  
 The new value of the **statementPoolingCacheSize** connection property.  

## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## Remarks  
 This method is available from JDBC driver version 6.4 and onward.
 
## See Also  
 [SQLServerDataSource Members](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource Class](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
