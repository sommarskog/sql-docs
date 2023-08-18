---
title: "Thread-Safety Notes on API Functions (ODBC Driver for Oracle)"
description: "Thread-Safety Notes on API Functions (ODBC Driver for Oracle)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "ODBC driver for Oracle [ODBC], threading"
  - "threading options [ODBC]"
  - "multiple concurrent statements [ODBC]"
---
# Thread-Safety Notes on API Functions (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  This feature will be removed in a future version of Windows. Avoid using this feature in new development work, and plan to modify applications that currently use this feature. Instead, use the ODBC driver provided by Oracle.  
  
 The Microsoft ODBC Driver for Oracle is thread-safe; however, Oracle does not allow multiple concurrent statements on a single connection. The driver enforces this restriction. In other words, in multithreaded applications, although any thread can call into the ODBC Driver for Oracle at any time, the driver blocks any other thread from the driver on the same connection until the original thread leaves the driver.  
  
 The driver does not block if there are two statements on two different connections. However, if there is a single connection with two statements, there is potential for blocking.
