---
title: "SQLTables (Paradox Driver)"
description: "SQLTables (Paradox Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "Paradox driver [ODBC], SQLTables"
  - "SQLTables function [ODBC], Paradox Driver"
---
# SQLTables (Paradox Driver)
> [!NOTE]  
>  This topic provides Paradox Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argument|Comments|  
|--------------|--------------|  
|*szTableOwner*|The only valid argument for *szTableOwner* is NULL because none of the drivers support owner names. With *szTableOwner* set to NULL, all tables are returned. NULL is returned in the TABLE_OWNER column.|  
|*szTableQualifier*|In the TABLE_QUALIFIER column, **SQLTables** will return the path to a directory.|  
|*SzTableType*|For Paradox files, "TABLE" is the only table type supported.|  
  
## See Also  
 [SQLTables Function](../../odbc/reference/syntax/sqltables-function.md)
