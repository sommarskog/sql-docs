---
title: "getSubString Method (SQLServerNClob)"
description: "getSubString Method (SQLServerNClob)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
---
# getSubString Method (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retrieves a copy of the specified substring in the **NCLOB** based on the specified starting position and the number of characters to copy.  
  
## Syntax  
  
```  
  
public java.lang.String getSubString(long pos,  
                                  int length)  
```  
  
#### Parameters  
 *pos*  
  
 The first character of the substring to be extracted. The first character is at position 1.  
  
 *length*  
  
 The number of consecutive characters to be copied.  
  
## Return Value  
 A **String** that is the specified substring in the **NCLOB**.  
  
## Exceptions  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## Remarks  
 This getSubString method is specified by the getSubString method in the java.sql.NClob interface.  
  
 Trying to get zero characters from a null or zero-length NCLOB returns an empty string. Trying to get any length of characters at any position other than position 1 in a zero-length NCLOB will cause a position exception to be thrown.  
  
## See Also  
 [SQLServerNClob Methods](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob Members](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob Class](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
