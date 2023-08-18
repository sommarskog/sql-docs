---
title: "Supported Data Types (Visual FoxPro ODBC Driver)"
description: "Supported Data Types (Visual FoxPro ODBC Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "Visual FoxPro ODBC driver [ODBC], data types"
  - "FoxPro ODBC driver [ODBC], data types"
  - "data types [ODBC], Visual FoxPro ODBC driver"
---
# Supported Data Types (Visual FoxPro ODBC Driver)
The list of data types supported by the driver are presented through the ODBC API and in Microsoft Query.  
  
## Data Types in C Applications  
 You can obtain a list of data types supported by the Visual FoxPro ODBC Driver by using the [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) function in C or C++ applications.  
  
## Data Types in Applications Using Microsoft Query  
 If your application uses Microsoft Query to create a new table on a Visual FoxPro data source, Microsoft Query displays the **New Table Definition** dialog box. Under **Field Description**, the **Type** box lists [Visual FoxPro field data types](../../odbc/microsoft/visual-foxpro-field-data-types.md), represented by single characters.
