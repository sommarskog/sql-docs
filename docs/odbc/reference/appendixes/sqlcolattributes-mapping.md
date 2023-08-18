---
title: "SQLColAttributes Mapping"
description: "SQLColAttributes Mapping"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "mapping deprecated functions [ODBC], SQLColAttributes"
  - "SQLColAttribute function [ODBC], mapping"
---
# SQLColAttributes Mapping
When an application calls **SQLColAttributes** through an ODBC *3.x* driver, the call to **SQLColAttributes** is mapped to **SQLColAttribute** as follows:  
  
> [!NOTE]
>  The prefix used in *FieldIdentifier* values in ODBC *3.x* has been changed from that used in ODBC *2.x*. The new prefix is "SQL_DESC"; the old prefix was "SQL_COLUMN".  
  
1.  If the application is an ODBC *2.x* application, *fDescType* is SQL_COLUMN_TYPE, and the returned type is a concise DATETIME type, the Driver Manager maps the return values for date, time, and timestamp codes.  
  
2.  If *fDescType* is SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE, or SQL_COLUMN_COUNT, the Driver Manager calls **SQLColAttribute** in the driver with the *FieldIdentifier* argument mapped to SQL_DESC_NAME, SQL_DESC_NULLABLE, or SQL_DESC_COUNT, as appropriate*.* All other values of *fDescType* are passed through to the driver.  
  
 An ODBC *3.x* driver must support all the ODBC *3.x* *FieldIdentifiers* listed for **SQLColAttribute**.  
  
 An ODBC *3.x* driver must support SQL_COLUMN_PRECISION and SQL_DESC_PRECISION, SQL_COLUMN_SCALE and SQL_DESC_SCALE, and SQL_COLUMN_LENGTH and SQL_DESC_LENGTH. These values are different because precision, scale, and length are defined differently in ODBC *3.x* than they were in ODBC *2.x*. For more information, see [Column Size, Decimal Digits, Transfer Octet Length, and Display Size](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) in Appendix D: Data Types.
