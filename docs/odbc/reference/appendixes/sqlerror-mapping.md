---
title: "SQLError Mapping"
description: "SQLError Mapping"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "mapping deprecated functions [ODBC], SQLError"
  - "SQLError function [ODBC], mapping"
---
# SQLError Mapping
When an application calls **SQLError** through an ODBC *3.x* driver, the call to  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 is mapped to  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 with the *HandleType* argument set to the value SQL_HANDLE_ENV, SQL_HANDLE_DBC, or SQL_HANDLE_STMT, as appropriate, and the *Handle* argument set to the value in *henv*, *hdbc*, or *hstmt*, as appropriate. The *RecNumber* argument is determined by the Driver Manager.
