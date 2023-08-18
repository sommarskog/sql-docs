---
title: "Visual FoxPro Terminology"
description: "Visual FoxPro Terminology"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "Visual FoxPro ODBC driver [ODBC], glossary"
  - "FoxPro ODBC driver [ODBC], glossary"
---
# Visual FoxPro Terminology
**database**  
 In Visual FoxPro, a database file has a .dbc extension and can contain one or more **tables**.  
  
 **database table**  
 In Visual FoxPro, a table that is associated with a database. Contrast **free table**.  
  
 **free table**  
 In Visual FoxPro, a table that is not associated with a database.  
  
 A .dbf file created in FoxPro version 2.x is a free table unless it is converted to a Visual FoxPro table and added to a Visual FoxPro database. Contrast **database table**.  
  
 **preparable SQL statement**  
 A SQL statement that has not already been processed by the **SQLPrepare** function. For more information about this function with the Visual FoxPro ODBC Driver, see [SQLPrepare (Visual FoxPro ODBC Driver)](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md).  
  
 **table**  
 In Visual FoxPro, records are stored in a table. Each row of a table represents a record, and the columns of the table represent the fields of the record. Each Visual FoxPro table is stored in its own file with a .dbf extension. Visual FoxPro tables can be associated with a database.  
  
 FoxPro version 2.*x* tables are not associated with a database.
