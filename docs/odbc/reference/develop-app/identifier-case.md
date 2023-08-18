---
title: "Identifier Case"
description: "Identifier Case"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "SQL statements [ODBC], interoperability"
  - "identifiers [ODBC], case"
  - "interoperability of SQL statements [ODBC], identifier case"
---
# Identifier Case
In SQL statements and catalog function arguments, identifiers and quoted identifiers can be either case-sensitive or not, which an application can determine by calling **SQLGetInfo** with the SQL_IDENTIFIER_CASE and SQL_QUOTED_IDENTIFIER_CASE options.  
  
 Each of these options has four possible return values: one stating that the identifier or quoted identifier case is sensitive and three stating that it is not sensitive. The three values that are not case-sensitive further describe the case in which identifiers are stored in the system catalog. How identifiers are stored in the system catalog is relevant only for display purposes, such as when an application displays the results of a catalog function; it does not change the case-sensitivity of identifiers.
