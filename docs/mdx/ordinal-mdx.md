---
title: "Ordinal (MDX)"
description: "Ordinal (MDX)"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# Ordinal (MDX)


  Returns the zero-based ordinal value associated with a level.  
  
## Syntax  
  
```  
  
Level_Expression.Ordinal   
```  
  
## Arguments  
 *Level_Expression*  
 A valid Multidimensional Expressions (MDX) expression that returns a level.  
  
## Remarks  
 The **Ordinal** function is frequently used in conjunction with the **IIF** and **CurrentMember** functions to conditionally display different values at different hierarchy levels, based on the ordinal position of each specific cell in the query result. For example, you can use the **Ordinal** function to perform calculations at certain levels and display a default value of "N/A" at other levels.  
  
## Example  
 The following example returns the ordinal number for the Calendar Quarter level in the Calendar hierarchy.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## See Also  
 [MDX Function Reference &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
