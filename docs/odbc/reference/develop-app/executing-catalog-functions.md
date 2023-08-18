---
title: "Executing Catalog Functions"
description: "Executing Catalog Functions"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "catalog functions [ODBC], executing"
  - "functions [ODBC], catalog functions"
---
# Executing Catalog Functions
Because a catalog function creates a result set, it is equivalent to executing any result set-generating SQL statement. In fact, catalog functions are often implemented by executing predefined SQL statements or calling predefined procedures that are shipped with the driver or DBMS. Almost anything that applies to SQL statements that create result sets also applies to catalog functions. For example, the SQL_ATTR_MAX_ROWS statement attribute limits the number of rows returned by the catalog function, just as it limits the number of rows returned by a **SELECT** statement.  
  
 To execute a catalog function, an application just calls the function.  
  
 For more information about catalog functions, see [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).
