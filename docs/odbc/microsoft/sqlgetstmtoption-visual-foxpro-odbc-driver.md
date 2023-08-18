---
title: "SQLGetStmtOption (Visual FoxPro ODBC Driver)"
description: "SQLGetStmtOption (Visual FoxPro ODBC Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver"
---
# SQLGetStmtOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  This topic contains Visual FoxPro ODBC Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Support: Full  
  
 ODBC API Conformance: Level One  
  
 Returns the current setting of a statement option.  
  
|*FOption*|Returns|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|32-bit integer value that is the bookmark for the current record number|  
|SQL_ROW_NUMBER|32-bit integer specifying the position of the current row within the result set|  
|SQL_TRANSLATE_DLL|Error: "Driver not capable"|  
  
 The Visual FoxPro ODBC Driver has no translation DLLs.  
  
 For more information, see [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) in the *ODBC Programmer's Reference*.
