---
title: "Machine Data Sources"
description: "Machine Data Sources"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "machine data sources [ODBC]"
  - "data sources [ODBC], machine"
---
# Machine Data Sources
*Machine data sources* are stored on the system with a user-defined name. Associated with the data source name is all of the information the Driver Manager and driver need to connect to the data source. For an Xbase data source, this might be the name of the Xbase driver, the full path of the directory containing the Xbase files, and some options that tell the driver how to use those files, such as single-user mode or read-only. For an Oracle data source, this might be the name of the Oracle driver, the server where the Oracle DBMS resides, the SQL*Net connection string that identifies the SQL\*Net driver to use, and the system ID of the database on the server.
