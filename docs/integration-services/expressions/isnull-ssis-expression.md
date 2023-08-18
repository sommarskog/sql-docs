---
title: "ISNULL (SSIS Expression)"
description: "ISNULL (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "null values [Integration Services]"
  - "ISNULL function"
---
# ISNULL (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns a Boolean result based on whether an expression is null.  
  
## Syntax  
  
```  
  
ISNULL(expression)  
```  
  
## Arguments  
 *expression*  
 Is a valid expression of any data type.  
  
## Result Types  
 DT_BOOL  
  
## Expression Examples  
 This example returns TRUE if the **DiscontinuedDate** column contains a null value.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 This example returns "Unknown last name" if the value in the **LastName** column is null, otherwise it returns the value in **LastName**.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 This example always returns TRUE if the **DaysToManufacture** column is null, regardless of the value of the variable **AddDays**.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## See Also  
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  
