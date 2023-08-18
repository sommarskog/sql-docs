---
title: "REPLICATE (SSIS Expression)"
description: "REPLICATE (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "REPLICATE function"
---
# REPLICATE (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns a character expression that is replicated a number of times. The *times* argument must evaluate to an integer.  
  
> [!NOTE]  
>  The REPLICATE function frequently uses long strings, and therefore is more likely to incur the 4000-character limit on expression length. If the evaluation result of an expression has the Integration Services data type DT_WSTR or DT_STR, the expression will be truncated at 4000 characters. If the result type of a sub-expression is DT_STR or DT_WSTR, that sub-expression likewise will be truncated to 4000 characters, regardless of the overall expression result type. The consequences of truncation can be handled gracefully or cause a warning or an error. For more information, see [Syntax &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md).  
  
## Syntax  
  
```  
  
REPLICATE(character_expression,times)  
```  
  
## Arguments  
 *character_expression*  
 Is a character expression to replicate.  
  
 *times*  
 Is an integer expression that specifies the number of times *character_expression* is replicated.  
  
## Result Types  
 DT_WSTR  
  
## Remarks  
 If *times* is zero, the function returns a zero-length string.  
  
 If *times* is a negative number, the function returns an error.  
  
 The *times* argument can also use variables and columns.  
  
 REPLICATE works only with the DT_WSTR data type. A *character_expression* argument that is a string literal or a data column with the DT_STR data type is implicitly cast to the DT_WSTR data type before REPLICATE performs its operation. Other data types must be explicitly cast to the DT_WSTR data type. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md) and [Cast &#40;SSIS Expression&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 REPLICATE returns a null result if either argument is null.  
  
## Expression Examples  
 This example replicates a string literal three times. The return result is "Mountain BikeMountain BikeMountain Bike".  
  
```  
REPLICATE("Mountain Bike", 3)  
```  
  
 This example replicates values in the **Name** column by the value in the **Times** variable. If **Times** is 3 and **Name** is Touring Front Wheel, the return result is Touring Front WheelTouring Front WheelTouring Front Wheel.  
  
```  
REPLICATE(Name, @Times)  
```  
  
 This example replicates the value in the **Name** variable by the value in the **Times** column. **Times** has a non-integer data type and the expression includes an explicit cast to an integer data type. If **Name** contains Helmet and **Times** is 2, the return result is "HelmetHelmet".  
  
```  
REPLICATE(@Name, (DT_I4(Times))  
```  
  
## See Also  
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
