---
title: "Using Logical Functions"
description: "Using Logical Functions"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# Using Logical Functions


  A logical function performs a logical operation or comparison on objects and expressions and returns a Boolean value. Logical functions are essential in Multidimensional Expressions (MDX) to determine the position of a member.  
  
 The most commonly used logical function is the **IsEmpty** function. For more information on how to use the **IsEmpty** function, see [Working with Empty Values](../mdx/working-with-empty-values.md).  
  
 The following query shows how to use the **IsLeaf** and **IsAncestor** functions:  
  
 `WITH`  
  
 `//Returns true if the CurrentMember on Calendar is a leaf member, ie it has no children`  
  
 `MEMBER MEASURES.[IsLeafDemo] AS IsLeaf([Date].[Calendar].CurrentMember)`  
  
 `//Returns true if the CurrentMember on Calendar is an Ancestor of July 1st 2001`  
  
 `MEMBER MEASURES.[IsAncestorDemo] AS IsAncestor([Date].[Calendar].CurrentMember, [Date].[Calendar].[Date].&[1])`  
  
 `SELECT{MEASURES.[IsLeafDemo],MEASURES.[IsAncestorDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## See Also  
 [Functions &#40;MDX Syntax&#41;](../mdx/functions-mdx-syntax.md)  
  
  
