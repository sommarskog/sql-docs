---
title: "Fetching Rows with SQLBulkOperations"
description: "Fetching Rows with SQLBulkOperations"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "data updates [ODBC], bookmarks"
  - "SQLBulkOperations function [ODBC], fetching rows"
  - "data updates [ODBC], SQLBulkOperations"
  - "bookmarks [ODBC]"
  - "updating data [ODBC], bookmarks"
  - "updating data [ODBC], SQLBulkOperations"
---
# Fetching Rows with SQLBulkOperations
Data can be refetched into a rowset using bookmarks by a call to **SQLBulkOperations.** The rows to be fetched are identified by the bookmarks in a bound bookmark column. Columns with a value of SQL_COLUMN_IGNORE are not fetched.  
  
 To perform bulk fetches with **SQLBulkOperations**, the application does the following:  
  
1.  Retrieves and caches the bookmarks of all rows to be updated. If there is more than one bookmark and column-wise binding is used, the bookmarks are stored in an array; if there is more than one bookmark and row-wise binding is used, the bookmarks are stored in an array of row structures.  
  
2.  Sets the SQL_ATTR_ROW_ARRAY_SIZE statement attribute to the number of rows to fetch and binds the buffer containing the bookmark value, or the array of bookmarks, to column 0.  
  
3.  Sets the value in the length/indicator buffer of each column as necessary. This is the byte length of the data or SQL_NTS for columns bound to string buffers, the byte length of the data for columns bound to binary buffers, and SQL_NULL_DATA for any columns to be set to NULL. The application sets the value in the length/indicator buffer of those columns that are to be set to their default (if one exists) or NULL (if one does not) to SQL_COLUMN_IGNORE.  
  
4.  Calls **SQLBulkOperations** with the *Operation* argument set to SQL_FETCH_BY_BOOKMARK.  
  
 There is no need for the application to use the row operation array to prevent the operation to be performed on certain columns. The application selects the rows it wants to fetch by copying only the bookmarks for those rows into the bound bookmark array.
