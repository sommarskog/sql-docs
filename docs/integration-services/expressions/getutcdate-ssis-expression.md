---
title: "GETUTCDATE (SSIS Expression)"
description: "GETUTCDATE (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "dates [Integration Services], GETUTCDATE"
  - "current date"
  - "UTC time"
  - "GETUTCDATE function"
---
# GETUTCDATE (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns the current date of the system in UTC time (Universal Time Coordinate or Greenwich Mean Time) using a DT_DBTIMESTAMP format. The GETUTCDATE function takes no arguments.  
  
## Syntax  
  
```  
  
GETUTCDATE()  
```  
  
## Arguments  
 None  
  
## Result Types  
 DT_DBTIMESTAMP  
  
## Expression Examples  
 This example returns the year of the current date in UTC time.  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 This example returns the number of days between a date in the **ModifiedDate** column and the current UTC date.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 This example adds three months to the current UTC date.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## See Also  
 [GETDATE &#40;SSIS Expression&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
