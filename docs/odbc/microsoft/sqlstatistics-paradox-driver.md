---
title: "SQLStatistics (Paradox Driver)"
description: "SQLStatistics (Paradox Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "Paradox driver [ODBC], SQLStatistics"
  - "SQLStatistics function [ODBC], Paradox Driver"
---
# SQLStatistics (Paradox Driver)
> [!NOTE]  
>  This topic provides Paradox Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Column|Comments|  
|------------|--------------|  
|TABLE_QUALIFIER|The path to a directory.<br /><br /> Pattern matching is not supported in the *szTableQualifier* argument.|  
|TABLE_OWNER|NULL is returned in this column because owner name is not supported.|  
|TABLE_NAME|Undelimited table name.<br /><br /> Pattern matching is not supported in the *szTableName* argument.|  
|INDEX_QUALIFIER|NULL is always returned.|  
|INDEX_NAME|Index-dependent.|  
|TYPE|Only SQL_TABLE_STAT or SQL_INDEX_OTHER will be returned for TYPE.|  
|SEQ_IN_INDEX|Index-dependent.|  
|COLUMN_NAME|Index-dependent.|  
|COLLATION|Index-dependent.|  
|PAGES|NULL is always returned.|  
  
 Filtering is based on uniqueness (the *fUnique* argument). The *fAccuracy* parameter is ignored.
