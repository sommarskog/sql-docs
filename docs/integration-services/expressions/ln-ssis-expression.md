---
title: "LN (SSIS Expression)"
description: "LN (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "LN function"
  - "natural logarithm of expression [Integration Services]"
---
# LN (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns the natural logarithm of a numeric expression.  
  
## Syntax  
  
```  
  
LN(numeric_expression)  
```  
  
## Arguments  
 *numeric_expression*  
 Is a valid non-zero and non-negative numeric expression.  
  
## Result Types  
 DT_R8  
  
## Remarks  
 The numeric expression is cast to the DT_R8 data type before the logarithm is computed. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 If *numeric_expression* evaluates to zero or a negative value, the return result is null.  
  
## Expression Examples  
 This example uses a numeric literal. The function returns the value 3.737766961828337.  
  
```  
LN(42)  
```  
  
 This example uses the column **Length**. If the column value is 53.99, the function returns 3.9887988442302.  
  
```  
LN(Length)   
```  
  
 This example uses the variable **Length**. The variable must have a numeric data type or the expression must include an explicit cast to a numeric data type. If **Length** is 234.567, the function returns 5.45774126708797.  
  
```  
LN(@Length)   
```  
  
## See Also  
 [LOG &#40;SSIS Expression&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
