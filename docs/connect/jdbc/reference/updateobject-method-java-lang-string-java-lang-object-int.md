---
title: "updateObject Method (java.lang.String, java.lang.Object, int)"
description: "updateObject Method (java.lang.String, java.lang.Object, int)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
apilocation: "sqljdbc.jar"
apiname: "SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)"
apitype: "Assembly"
---
# updateObject Method (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Updates the designated column with an **Object** value given the column name and scale.  
  
## Syntax  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### Parameters  
 *columnName*  
  
 A **String** that contains the column name.  
  
 *obj*  
  
 An **Object** value.  
  
 *scale*  
  
 For java.sql.Types.DECIMAL or java.sql.Types.NUMERIC types, this is the number of digits after the decimal point. For all other types this value is ignored.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This updateObject method is specified by the updateObject method in the java.sql.ResultSet interface.  
  
## See Also  
 [updateObject Method &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet Members](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet Class](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
