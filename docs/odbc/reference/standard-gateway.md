---
title: "Standard Gateway"
description: "Standard Gateway"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "ODBC [ODBC], database access"
  - "SQL [ODBC], database access"
  - "database access [ODBC]"
  - "standardizing database access [ODBC], gateways"
  - "standard gateways [ODBC]"
  - "gateways [ODBC]"
---
# Standard Gateway
A *gateway* is a piece of software that causes one DBMS to look like another. That is, the gateway accepts the programming interface, SQL grammar, and data stream protocol of a single DBMS and translates it to the programming interface, SQL grammar, and data stream protocol of the hidden DBMS. For example, applications written to use Microsoft® SQL Server™ can also access DB2 data through the Micro Decisionware DB2 Gateway; this product causes DB2 to look like SQL Server. When gateways are used, a different gateway must be written for each target database.  
  
 Although gateways are limited by architectural differences among DBMSs, they are a good candidate for standardization. However, if all DBMSs are to standardize on the programming interface, SQL grammar, and data stream protocol of a single DBMS, whose DBMS is to be chosen as the standard? Certainly no commercial DBMS vendor is likely to agree to standardize on a competitor's product. And if a standard programming interface, SQL grammar, and data stream protocol are developed, no gateway is needed.
