---
title: "Connection Strings"
description: "Connection Strings"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "data sources [ODBC], connection functions"
  - "connecting to driver [ODBC], connection strings"
  - "functions [ODBC], data source or driver connections"
  - "connection strings [ODBC], about connection strings"
  - "connecting to data source [ODBC], connection strings"
  - "connecting to data source [ODBC], functions"
  - "connecting to driver [ODBC], functions"
  - "connection functions [ODBC]"
  - "ODBC drivers [ODBC], connection functions"
---
# Connection Strings
A connection string contains information used for establishing a connection. A complete connection string contains all the information needed to establish a connection. The connection string is a series of keyword/value pairs separated by semicolons. (For the complete syntax of a connection string, see the [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) function description.) The connection string is used by:  
  
-   **SQLDriverConnect**, which completes the connection string by interaction with the user.  
  
-   **SQLBrowseConnect**, which completes the connection string iteratively with the data source.  
  
 **SQLConnect** does not use a connection string; using **SQLConnect** is analogous to connecting using a connection string with exactly three keyword/value pairs (for data source name and, optionally, user ID and password).
