---
title: "~ (Bitwise Not) (SSIS Expression)"
description: "~ (Bitwise Not) (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "bitwise NOT (~)"
  - "~ (bitwise NOT)"
---
# ~ (Bitwise Not) (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Performs a bitwise negation of an integer. This operator can be applied to signed and unsigned integer data types.  
  
## Syntax  
  
```  
  
~integer_expression  
  
```  
  
## Arguments  
 *integer_expression*  
 Is any valid expression of an integer data type. *integer*_*expression* is an integer that is transformed into a binary number for the bitwise operation. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Result Types  
 Returns the data type of *integer_expression.*  
  
## Remarks  
 None  
  
## Expression Examples  
 This example performs a bitwise ~ (NOT) operation on the number 170 (0000 0000 1010 1010). The number is a signed integer.  
  
```  
  
~ 170  
```  
  
 The expression evaluates to -170 (1111111101010101).  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## See Also  
 [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operators &#40;SSIS Expression&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
