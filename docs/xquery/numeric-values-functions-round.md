---
title: "round Function (XQuery)"
description: Learn about the XQuery function round() that returns the number not having a fractional part that is closest to the specified argument.
author: "rothja"
ms.author: "jroth"
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "language-reference"
helpviewer_keywords:
  - "fn:round function"
  - "round function [XQuery]"
dev_langs:
  - "XML"
---
# Numeric Values Functions - round
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sqlserver.md)]

  Returns the number not having a fractional part that is closest to the argument. If there is more than one number like that, the one that is closest to positive infinity is returned. For example:  
  
 If the argument is 2.5, **round()** returns 3.  
  
 If the argument is 2.4999, **round()** returns 2.  
  
 If the argument is -2.5, **round()** returns -2.  
  
 If the argument is an empty sequence, **round()** returns the empty sequence.  
  
## Syntax  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## Arguments  
 *$arg*  
 Number to which the function is applied.  
  
## Remarks  
 If the type of *$arg* is one of the three numeric base types, **xs:float**, **xs:double**, or **xs:decimal**, the return type is same as the *$arg* type. If the type of *$arg* is a type that is derived from one of the numeric types, the return type is the base numeric type.  
  
 If input to the **fn:floor**, **fn:ceiling**, or **fn:round** functions is **xdt:untypedAtomic**, untyped data, it is implicitly cast to **xs:double**.  
  
 Any other type generates a static error.  
  
## Examples  
 This topic provides XQuery examples against XML instances stored in various **xml** type columns in the AdventureWorks database.  
  
 You can use the working sample in the [ceiling function (XQuery)](../xquery/numeric-values-functions-ceiling.md) for the **round()** XQuery function. All you have to do is replace the **ceiling()** function in the query with the **round()** function.  
  
## Implementation Limitations  
 These are the limitations:  
  
-   The **round()** function maps integer values to xs:decimal.  
  
-   The **round()** function of xs:double and xs:float values between -0.5e0 and -0e0 are mapped to 0e0 instead of -0e0.  
  
## See Also  
 [floor Function &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling Function &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
