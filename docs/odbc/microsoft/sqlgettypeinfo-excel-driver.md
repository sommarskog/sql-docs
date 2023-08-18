---
title: "SQLGetTypeInfo (Excel Driver)"
description: "SQLGetTypeInfo (Excel Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "SQLGetTypeInfo function [ODBC], Excel Driver"
  - "Excel driver [ODBC], SQLGetTypeInfo"
---
# SQLGetTypeInfo (Excel Driver)
> [!NOTE]  
>  This topic provides Excel Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 The name of the type (TYPE_NAME) returned in the table produced by **SQLGetTypeInfo** will be the name most commonly used by the data source.  
  
 SQL_ALL_EXCEPT_LIKE will be returned in the SEARCHABLE column for the Byte, Counter, Double, Single, Long, and Short data types. (The LIKE capability can be achieved by converting the value to a character using the ODBC canonical conversion functions, then performing the comparison.)  
  
 When the Microsoft Excel driver is used, the ODBC type names are returned in the TYPE_NAME column that is returned by **SQLGetTypeInfo**.
