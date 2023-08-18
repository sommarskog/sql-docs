---
title: "setBinaryStream Method  to input stream - long"
description: "setBinaryStream Method  (java.lang.String, java.io.InputStream, int)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerCallableStatement.setBinaryStream"
apitype: "Assembly"
---
# setBinaryStream Method  (java.lang.String, java.io.InputStream, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Sets the designated parameter to the specified input stream, which will have the specified number of bytes.  
  
## Syntax  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream value,  
                            int length)  
```  
  
#### Parameters  
 *parameterName*  
  
 A **String** that contains the name of the parameter.  
  
 *value*  
  
 An InputStream object.  
  
 *length*  
  
 An **int** that indicates the length in number of bytes.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This setBinaryStream method is specified by the setBinaryStream method in the java.sql.CallableStatement interface.  
  
 If the length of the stream is different than what is specified in the *length* parameter, the JDBC driver throws an exception when the row is updated or inserted.  
  
 If the length of the stream is unknown, the *length* parameter may be set to -1 to indicate that the driver should accept the stream regardless of its length. With sqljdbc4.jar, we recommend that you use the JDBC 4.0 method [setBinaryStream Method (java.lang.String, java.io.InputStream)](../../../connect/jdbc/reference/setbinarystream-method-java-lang-string-java-io-inputstream.md) when the application wants to update the column from a stream whose length is unknown.  
  
## See Also  
 [setBinaryStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement Members](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
