---
title: "setAsciiStream Method (int, java.io.InputStream, int)"
description: "setAsciiStream Method (int, java.io.InputStream, int)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerPreparedStatement.setAsciiStream"
apitype: "Assembly"
---
# setAsciiStream Method (int, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sets the designated parameter number to the given InputStream object with the given number of bytes.  
  
## Syntax  
  
```  
  
public final void setAsciiStream(int n,  
                                 java.io.InputStream x,  
                                 int length)  
```  
  
#### Parameters  
 *n*  
  
 An **int** that indicates the parameter number.  
  
 *x*  
  
 An InputStream object.  
  
 *length*  
  
 The number of bytes.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This setAsciiStream method is specified by the setAsciiStream method in the java.sql.PreparedStatement interface.  
  
 If the length of the stream is different than that specified in the *length* parameter, the JDBC driver throws an exception when the row is updated or inserted.  
  
 If the length of the stream is unknown, the *length* parameter may be set to -1 to indicate that the driver should accept the stream regardless of its length. With sqljdbc4.jar, we recommend that you use the JDBC 4.0 method [setAsciiStream Method &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) when the application wants to update the column from a stream whose length is unknown.  
  
## See Also  
 [setAsciiStream Method &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement Members](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
