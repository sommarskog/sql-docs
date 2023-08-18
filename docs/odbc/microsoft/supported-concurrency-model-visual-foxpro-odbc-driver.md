---
title: "Supported Concurrency Model (Visual FoxPro ODBC Driver)"
description: "Supported Concurrency Model (Visual FoxPro ODBC Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "Visual FoxPro ODBC driver [ODBC], concurrency"
  - "concurrency models [ODBC]"
  - "FoxPro ODBC driver [ODBC], concurrency"
---
# Supported Concurrency Model (Visual FoxPro ODBC Driver)
The Visual FoxPro ODBC Driver supports *read-only concurrency*. Your application can call [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) with a SQL_CONCURRENCY option of SQL_CONCUR_READ_ONLY.  
  
 For more information, see the [ODBC Programmer's Reference](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## read-only concurrency  
 The cursor cannot be updated.  
  
## row versioning  
 Essentially timestamp support, in which row versions are compared at update time.
