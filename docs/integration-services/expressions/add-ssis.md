---
title: "+ (Add) (SSIS)"
description: "+ (Add) (SSIS)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "+ (add)"
  - "add operator (+)"
  - "adding expressions"
---
# + (Add) (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Adds two numeric expressions.  
  
## Syntax  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## Arguments  
 *numeric_expression1, numeric_ expression2*  
 Is any valid expression of a numeric data type.  
  
## Result Types  
 Determined by data types of the two arguments. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Remarks  
 If either operand is null, the result is null.  
  
## Expression Examples  
 This example adds numeric literals.  
  
```  
5 + 6.09 + 7.0  
```  
  
 This example adds values in the **VacationHours** and **SickLeaveHours** columns.  
  
```  
VacationHours + SickLeaveHours  
```  
  
 This example adds a calculated value to the **StandardCost** column. The variable **Profit%** must be enclosed in brackets because the name includes the % character. For more information, see [Identifiers &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## See Also  
 [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operators &#40;SSIS Expression&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
