---
title: "LOWER (SSIS Expression)"
description: "LOWER (SSIS Expression)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "converting uppercase to lowercase"
  - "LOWER function"
  - "uppercase characters [Integration Services]"
  - "lowercase characters"
---
# LOWER (SSIS Expression)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Returns a character expression after converting uppercase characters to lowercase characters.  
  
## Syntax  
  
```  
  
LOWER(character_expression)  
```  
  
## Arguments  
 *character_expression*  
 Is a character expression to convert to lowercase characters.  
  
## Result Types  
 DT_WSTR  
  
## Remarks  
 LOWER works only with the DT_WSTR data type. A *character_expression* argument that is a string literal or a data column with the DT_STR data type is implicitly cast to the DT_WSTR data type before LOWER performs its operation. Other data types must be explicitly cast to the DT_WSTR data type. For more information, see [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md) and [Cast &#40;SSIS Expression&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LOWER returns a null result if the argument is null.  
  
## Expression Examples  
 This example converts a string literal to lowercase characters. The return result is "new york".  
  
```  
LOWER("New York")  
```  
  
 This example converts all characters from the **Color** input column, except the first character, to lowercase characters. If Color is YELLOW, the return result is "Yellow". For more information, see [SUBSTRING &#40;SSIS Expression&#41;](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 This example converts the value in the **CityName** variable to lowercase characters.  
  
```  
LOWER(@CityName)  
```  
  
## See Also  
 [UPPER &#40;SSIS Expression&#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [Functions &#40;SSIS Expression&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
