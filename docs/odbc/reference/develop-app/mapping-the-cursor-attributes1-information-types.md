---
title: "Mapping the Cursor Attributes1 Information Types"
description: "Mapping the Cursor Attributes1 Information Types"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "compatibility [ODBC], mapping cursor attributes1 information types"
  - "application upgrades [ODBC], mapping cursor attributes1 information types"
  - "mapping cursor attributes1 information types [ODBC]"
  - "backward compatibility [ODBC], mapping cursor attributes1 information types"
  - "upgrading applications [ODBC], mapping cursor attributes1 information types"
---
# Mapping the Cursor Attributes1 Information Types
When an ODBC 3.*x* application calls **SQLGetInfo** in an ODBC 2*.x* driver with the SQL_XXXX_CURSOR_ATTRIBUTES1 information type (for dynamic, forward-only, keyset-driver, or static cursors), the setting of the bits returned by Driver Manager depends on what the ODBC 2.*x* driver returns for the corresponding ODBC 2.*x* information types. The bits are set as shown in the following table.  
  
|Bit in<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Cursor type|ODBC 2.*x* information<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dynamic, keyset-driver, static|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dynamic, keyset-driver, static|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dynamic, keyset-driver, static|SQL_POS_OPERATIONS|
