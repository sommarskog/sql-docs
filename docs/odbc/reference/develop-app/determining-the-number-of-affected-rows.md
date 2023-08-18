---
title: "Determining the Number of Affected Rows"
description: "Determining the Number of Affected Rows"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "updating data [ODBC], number of rows affected"
  - "number of rows affected by update [ODBC]"
  - "data updates [ODBC], number of rows affected"
---
# Determining the Number of Affected Rows
After an application updates, deletes, or inserts rows, it can call **SQLRowCount** to determine how many rows were affected. **SQLRowCount** returns this value whether or not the rows were updated, deleted, or inserted by executing an **UPDATE**, **DELETE**, or **INSERT** statement, by executing a positioned update or delete statement, or by calling **SQLSetPos**.  
  
 If a batch of SQL statements is executed, the count of affected rows might be a total count for all statements in the batch or individual counts for each statement in the batch. For more information, see [Batches of SQL Statements](../../../odbc/reference/develop-app/batches-of-sql-statements.md) and [Multiple Results](../../../odbc/reference/develop-app/multiple-results.md).  
  
 The number of affected rows is also returned in the SQL_DIAG_ROW_COUNT diagnostic header field in the diagnostic area associated with the statement handle. However, the data in this field is reset after every function call on the same statement handle, whereas the value returned by **SQLRowCount** remains the same until a call to **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPrepare**, or **SQLSetPos**.
