---
title: "CustomData (MDX)"
description: "CustomData (MDX)"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# CustomData (MDX)


  Returns the value of the **CustomData** connection string property if defined; otherwise, **null**.  
  
## Syntax  
  
```  
  
CustomData()  
```  
  
## Return Value  
 The **CustomData** function can retrieve the **CustomData** connection string property and pass a configuration setting to be used by Multidimensional Expressions (MDX) functions and statements, such as [UserName (MDX)](../mdx/username-mdx.md) and [CALL Statement (MDX)](../mdx/mdx-data-manipulation-call.md). For example, this function can be used in a dynamic security expression to select the allowed/denied set members for the string value in the **CustomData** connection string property.  
  
## Example  
 The following query displays the value returned by the **CustomData** function in a calculated measure:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## See Also  
 [MDX Function Reference &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
