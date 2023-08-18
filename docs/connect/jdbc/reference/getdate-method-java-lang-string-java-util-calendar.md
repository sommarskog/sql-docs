---
title: "getDate Method (java.util.Calendar) parameter"
description: "getDate Method (java.lang.String, java.util.Calendar)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerCallableStatement.getDate (java.util.Calendar)"
apitype: "Assembly"
---
# getDate Method (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retrieves the value of the designated parameter as a java.sql.Date object in the Java programming language given the parameter name and Calendar object.  
  
## Syntax  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### Parameters  
 *sCol*  
  
 A **String** that contains the parameter name.  
  
 *cal*  
  
 A Calendar object.  
  
## Return Value  
 A Date object.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This getDate method is specified by the getDate method in the java.sql.CallableStatement interface.  
  
 This method returns a valid date part of a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime or smalldatetime data type, with the time part set to the Java time baseline of 00:00 (midnight).  
  
## See Also  
 [getDate Method &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement Members](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement Class](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
