---
title: "FirstChild (MDX)"
description: "FirstChild (MDX)"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# FirstChild (MDX)


  Returns the first child of a specified member.  
  
## Syntax  
  
```  
  
Member_Expression.FirstChild   
```  
  
## Arguments  
 *Member_Expression*  
 A valid Multidimensional Expressions (MDX) expression that returns a member.  
  
### Example  
 The following query returns the first child of fiscal year 2003 in the Fiscal hierarchy, which is the first semester of Fiscal Year 2003.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## See Also  
 [LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)   
 [MDX Function Reference &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
