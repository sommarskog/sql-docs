---
title: "Calling SQLSetPos to Insert Data"
description: "Calling SQLSetPos to Insert Data"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "compatibility [ODBC], SQLSetPos"
  - "SQLSetPos function [ODBC], inserting data"
  - "backward compatibility [ODBC], SqlSetPos"
---
# Calling SQLSetPos to Insert Data
When an ODBC *2.x* application working with an ODBC *3.x* driver calls **SQLSetPos** with an *Operation* argument of SQL_ADD, the Driver Manager does not map this call to **SQLBulkOperations**. If an ODBC *3.x* driver should work with an application that calls **SQLSetPos** with SQL_ADD, the driver should support that operation.  
  
 One major difference in behavior when **SQLSetPos** is called with SQL_ADD occurs when it is called in state S6. In ODBC *2.x*, the driver returned S1010 when **SQLSetPos** was called with SQL_ADD in state S6 (after the cursor has been positioned with **SQLFetch**). In ODBC *3.x*, **SQLBulkOperations** with an *Operation* of SQL_ADD can be called in state S6. A second major difference in behavior is that **SQLBulkOperations** with an *Operation* of SQL_ADD can be called in state S5, while **SQLSetPos** with an **Operation** of SQL_ADD cannot. For the statement transitions that can occur for the same call in ODBC *3.x*, see [Appendix B: ODBC State Transition Tables](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
