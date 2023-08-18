---
title: "SQLDriverConnect (Text File Driver)"
description: "SQLDriverConnect (Text File Driver)"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
helpviewer_keywords:
  - "SQLDriverConnect function [ODBC], Text File Driver"
  - "text file driver [ODBC], SQLDriverConnect"
---
# SQLDriverConnect (Text File Driver)
> [!NOTE]  
>  This topic provides Text File Driver-specific information. For general information about this function, see the appropriate topic under [ODBC API Reference](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** enables you to connect to a driver without creating a data source (DSN).  
  
 The following keywords are supported in the connection string for all drivers: **DSN**, **DBQ**, and **FIL**.  
  
 The following table shows the minimum keywords required to connect to each driver, and provides an example of keyword/value pairs used with **SQLDriverConnect**. For a full list of DRIVERID values, see [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  If DBQ or DefaultDir is not specified for the Text driver, the driver will connect to the current directory.  
  
|Driver|Keywords required|Examples|  
|------------|-----------------------|--------------|  
|Text|Driver|Driver={Microsoft Text Driver (*.txt;\*.csv)}; DefaultDir=c:\temp|
