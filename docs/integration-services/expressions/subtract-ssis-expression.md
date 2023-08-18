---
title: "- (Subtract) (SSIS Expression)"
description: "- (Subtract) (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "- (subtract)"
  - "subtract operator (-)"
---
# - (Subtract) (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Subtracts the second numeric expression from the first one.  
  
## Syntax  
  
```  
  
numeric_expression1 - numeric_expression2  
  
```  
  
## Arguments  
 *numeric_expression1, numeric_expression2*  
 Is any valid expression of a numeric data type. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Result Types  
 Determined by the data types of the two arguments. For more information, see [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Remarks  
 - Enclose the minus unary expression in parenthesis to ensure that the expression is evaluated in the correct order  

 - If either operand is null, the result is null.  
  
## Expression Examples  
 This example subtracts numeric literals.  
  
```  
5 - 6.09  
```  
  
 This example subtracts the value in the **StandardCost** column from the value in the **ListPrice** column.  
  
```  
ListPrice - StandardCost  
```  
  
 This example subtracts a calculated value from the **ListPrice** column. The variable **Discount%** must be enclosed in brackets because the name includes the % character. For more information, see [Identifiers &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## See Also  
 [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operators &#40;SSIS Expression&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
