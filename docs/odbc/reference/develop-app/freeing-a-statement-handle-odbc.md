---
title: "Freeing a Statement Handle ODBC"
description: "Freeing a Statement Handle ODBC"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "statement handles [ODBC]"
  - "handles [ODBC], statement"
  - "freeing statement handles [ODBC]"
---
# Freeing a Statement Handle ODBC
As mentioned earlier, it is more efficient to reuse statements than to drop them and allocate new ones. Before executing a new SQL statement on a statement, applications should be sure that the current statement settings are appropriate. These include statement attributes, parameter bindings, and result set bindings. Generally, parameters and result sets for the old SQL statement need to be unbound (by calling **SQLFreeStmt** with the SQL_RESET_PARAMS and SQL_UNBIND options) and rebound for the new SQL statement.  
  
 When the application has finished using the statement, it calls **SQLFreeHandle** to free the statement. After freeing the statement, it is an application programming error to use the statement's handle in a call to an ODBC function; doing so has undefined but probably fatal consequences.  
  
 When **SQLFreeHandle** is called, the driver releases the structure used to store information about the statement.  
  
 **SQLDisconnect** automatically frees all statements on a connection.
