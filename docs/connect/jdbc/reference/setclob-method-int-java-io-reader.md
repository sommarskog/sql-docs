---
title: "setClob Method (int, java.io.Reader)"
description: "setClob Method (int, java.io.Reader)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# setClob Method (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sets the designated parameter to the specified Reader object.  
  
## Syntax  
  
```  
  
public final void setClob(int parameterIndex,  
                          java.io.Reader reader)  
```  
  
#### Parameters  
 *parameterIndex*  
  
 An **int** that indicates the parameter index.  
  
 *reader*  
  
 A Reader object.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This setClob method is specified by the setClob method in the java.sql.PreparedStatement interface.  
  
## See Also  
 [setClob Method &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement Members](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
