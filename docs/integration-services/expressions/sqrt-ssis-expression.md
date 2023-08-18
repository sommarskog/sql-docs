---
title: "SQRT (SSIS Expression)"
description: "SQRT (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "SQRT function"
  - "square root of given expression"
---
# SQRT (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns the square root of a numeric expression.  
  
## Syntax  
  
```  
  
SQRT(numeric_expression)  
```  
  
## Arguments  
 *numeric_expression*  
 Is a numeric expression of any numeric data type. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Result Types  
 DT_R8  
  
## Remarks  
 SQRT returns a null result if the argument is null.  
  
 SQRT fails if the argument is a negative value.  
  
 The argument is cast to the DT_R8 data type before the square root operation.  
  
## Expression Examples  
 This example returns the square root of a numeric literal. The return result is 12.  
  
```  
SQRT(144)  
```  
  
 This example returns the square root of an expression, the result of subtracting values in the **Value1** and **Value2** columns.  
  
```  
SQRT(Value1 - Value2)  
```  
  
 This example returns the length of the third side of a right triangle by applying the SQUARE function to two variables and then calculating the square root of their sum. If **Side1** contains 3 and **Side2** contains 4, the SQRT function returns 5.  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  In expressions, variable names always include the \@ prefix.  
  
## See Also  
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
