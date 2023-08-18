---
title: "SQLSetScrollOptions Function"
description: "SQLSetScrollOptions Function"
author: David-Engel
ms.author: v-davidengel
ms.date: "07/18/2019"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
f1_keywords:
  - "SQLSetScrollOptions"
helpviewer_keywords:
  - "SQLSetScrollOptions function [ODBC]"
apilocation: "sqlsrv32.dll"
apiname: "SQLSetScrollOptions"
apitype: "dllExport"
---
# SQLSetScrollOptions Function
**Conformance**  
 Version Introduced: ODBC 1.0 Standards Compliance: Deprecated  
  
 **Summary**  
 In ODBC *3.x*, the ODBC 2.0 function **SQLSetScrollOptions** has been replaced by calls to **SQLGetInfo** and **SQLSetStmtAttr**.  
  
> [!NOTE]
>  For more information about what the Driver Manager maps this function to when an ODBC *2.x* application is working with an ODBC *3.x* driver, see [Mapping Deprecated Functions](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) in Appendix G: Driver Guidelines for Backward Compatibility.  
> 
> [!NOTE]
>  When the Driver Manager maps **SQLSetScrollOptions** for an application working with an ODBC *3.x* driver that does not support **SQLSetScrollOptions**, the Driver Manager sets the SQL_ROWSET_SIZE statement option, not the SQL_ATTR_ROW_ARRAY_SIZE statement attribute, to the *RowsetSize* argument in **SQLSetScrollOption**. As a result, **SQLSetScrollOptions** cannot be used by an application when fetching multiple rows by a call to **SQLFetch** or **SQLFetchScroll**. It can be used only when fetching multiple rows by a call to **SQLExtendedFetch**.  
  
## Remarks  
 If your application will run on a 64-bit operating system, see [ODBC 64-Bit Information](../../../odbc/reference/odbc-64-bit-information.md).  
  
## See Also  
 [ODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC Header Files](../../../odbc/reference/install/odbc-header-files.md)
