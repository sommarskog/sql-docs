---
title: "SQLExtendedFetch (Cursor Library)"
description: "SQLExtendedFetch (Cursor Library)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "SQLExtendedFetch function [ODBC], Cursor Library"
---
# SQLExtendedFetch (Cursor Library)
> [!IMPORTANT]  
>  This feature will be removed in a future version of Windows. Avoid using this feature in new development work and plan to modify applications that currently use this feature. Microsoft recommends using the driver's cursor functionality.  
  
 This topic discusses the use of the **SQLExtendedFetch** function in the cursor library. For general information about **SQLExtendedFetch**, see [SQLExtendedFetch Function](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 The cursor library implements **SQLExtendedFetch** by repeatedly calling **SQLFetch** in the driver.  
  
 The cursor library supports calling **SQLExtendedFetch** with a *FetchOrientation* of SQL_FETCH_BOOKMARK.  
  
 When the cursor library is used, calls to **SQLExtendedFetch** cannot be mixed with calls to either **SQLFetchScroll** or **SQLFetch**.
