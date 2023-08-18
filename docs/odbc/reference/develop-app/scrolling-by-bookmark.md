---
title: "Scrolling by Bookmark"
description: "Scrolling by Bookmark"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "result sets [ODBC], bookmarks"
  - "bookmarks [ODBC]"
  - "scrolling rows [ODBC]"
---
# Scrolling by Bookmark
When fetching rows with **SQLFetchScroll**, an application can use a bookmark as a basis for selecting the starting row. This is a form of absolute addressing because it does not depend on the current cursor position. To scroll to a bookmarked row, the application calls **SQLFetchScroll** with a *FetchOrientation* of SQL_FETCH_BOOKMARK. This operation uses the bookmark pointed to by the SQL_ATTR_FETCH_BOOKMARK_PTR statement attribute. It returns the rowset starting with the row identified by that bookmark. An application can specify an offset for this operation in the *FetchOffset* argument of the call to **SQLFetchScroll**. When an offset is specified, the first row of the returned rowset is determined by adding the number in the *FetchOffset* argument to the number of the row identified by the bookmark. This use of the *FetchOffset* argument is not supported when used with ODBC 2.*x* drivers; when an application calls **SQLFetchScroll** in an ODBC 2.*x* driver with *FetchOrientation* set to SQL_FETCH_BOOKMARK, the *FetchOffset* argument must be set to 0.
