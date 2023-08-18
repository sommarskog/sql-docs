---
title: "SQLTransact Mapping"
description: "SQLTransact Mapping"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "mapping deprecated functions [ODBC], SQLTransact"
  - "SQLTransact function [ODBC], mapping"
---
# SQLTransact Mapping
**SQLTransact** is now replaced by **SQLEndTran**. The major difference between the two functions is that **SQLEndTran** contains an argument *HandleType*, which specifies the scope of the work to be done. The *HandleType* argument can specify the environment or the connection handle. The following call to **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 is mapped to  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 if *ConnectionHandle* is not equal to SQL_NULL_HDBC. The *ConnectionHandle* argument is set to the value of *hdbc*.  
  
 **SQL_Transact** is mapped to  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 if *ConnectionHandle* is equal to SQL_NULL_HDBC. The *EnvironmentHandle* argument is set to the value of *henv*.  
  
 In both of the preceding cases, the *CompletionType* argument is set to the same value as *fType*.
