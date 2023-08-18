---
title: "REVERSE (SSIS Expression)"
description: "REVERSE (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "REVERSE function"
  - "reverse character expressions"
---
# REVERSE (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns a character expression in reverse order.  
  
## Syntax  
  
```  
  
REVERSE(character_expression)  
```  
  
## Arguments  
 *character_expression*  
 Is a character expression to be reversed.  
  
## Result Types  
 DT_WSTR  
  
## Remarks  
 The *character_expression* argument must have the DT_WSTR data type.  
  
 REVERSE returns a null result if *character_expression* is null.  
  
## Expression Examples  
 This example uses a string literal. The return result is "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 This example uses a variable. If **Name** contains Touring Bike, the return result is "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## See Also  
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
