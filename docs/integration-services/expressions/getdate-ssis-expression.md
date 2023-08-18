---
title: "GETDATE (SSIS Expression)"
description: "GETDATE (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "current date"
  - "GETDATE function"
  - "dates [Integration Services], GETDATE"
---
# GETDATE (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns the current date of the system in a DT_DBTIMESTAMP format. The GETDATE function takes no arguments.  
  
> [!NOTE]  
>  The length of the return result from the GETDATE function is 29 characters.  
  
## Syntax  
  
```  
  
GETDATE()  
```  
  
## Arguments  
 None  
  
## Result Types  
 DT_DBTIMESTAMP  
  
## Expression Examples  
 This example returns the year of the current date.  
  
```  
DATEPART("year",GETDATE())  
```  
  
 This example returns the number of days between a date in the **ModifiedDate** column and the current date.  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 This example adds three months to the current date.  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## See Also  
 [GETUTCDATE &#40;SSIS Expression&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
