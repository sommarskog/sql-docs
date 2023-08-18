---
title: "Tracing"
description: "Tracing"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "tracing options [ODBC], about tracing"
  - "driver manager [ODBC], tracing"
---
# Tracing
The ODBC Driver Manager has a trace facility that allows the sequence of function calls made by an ODBC application to be recorded and transcribed into a log file. Tracing is performed by a trace DLL that captures calls between the application and the Driver Manager, and between the Driver Manager and the driver. This method of tracing replaces the tracing performed by the ODBC 2*.x* Driver Manager and the tracing performed in ODBC 2*.x* by ODBC Spy.  
  
 This section contains the following topics.  
  
-   [Trace DLL](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Trace File](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [Enabling Tracing](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Dynamic Tracing](../../../odbc/reference/develop-app/dynamic-tracing.md)
