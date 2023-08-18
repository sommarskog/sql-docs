---
title: ODBC Test
description: ODBC Test is an ODBC-enabled application that you can use to test ODBC drivers and the ODBC Driver Manager.
author: David-Engel
ms.author: v-davidengel
ms.date: 09/01/2020
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "ODBC test [ODBC]"
  - "ODBC drivers [ODBC], testing"
  - "gtrtst32.dll"
  - "gtrts32w.dll [ODBC]"
  - "odbct32w.exe [ODBC]"
  - "odbcte32.exe [ODBC]"
  - "testing ODBC drivers [ODBC]"
---

# ODBC Test

## About

Microsoft® ODBC Test is an ODBC-enabled application that you can use to test ODBC drivers and the ODBC Driver Manager. ODBC Test is included as part of the [Microsoft Data Access Components (MDAC) 2.8 Software Development Kit](https://www.microsoft.com/download/details.aspx?id=21995).

ODBC 3.51 includes both ANSI and Unicode-enabled versions of ODBC Test. The corresponding files are as follows:

- `Odbcte32.exe` and `Gtrtst32.dll`, for the ANSI version.

- `Odbct32w.exe` and `Gtrts32w.dll`, for the Unicode version.

To use ODBC Test, you must understand the ODBC API, the C language, and SQL. For more information about the ODBC API, see the [ODBC Programmer's Reference](../odbc/reference/odbc-programmer-s-reference.md).

Help topics that were formerly included within this section of the documentation are now contained within the ODBC Test program. Open `Odbcte32.exe` or `Odbct32w.exe`, open the **Help** menu, and then click **Help Topics**.

Note that the 64-bit versions of these applications, meant for 64-bit Microsoft Windows operating systems, have the same names as the 32-bit versions, even though they are separate files. i.e. the name for the Unicode version of the 64-bit version of ODBC Test is `odbct32w.exe`.

## Open source

ODBC Test is open source. To view the code and build the latest version of ODBC Test yourself, go to the [GitHub repository for ODBC Test](https://github.com/microsoft/ODBCTest).
