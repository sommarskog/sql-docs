---
title: "Extract (MDX)"
description: "Extract (MDX)"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# Extract (MDX)


  Returns a set of tuples from extracted hierarchy elements.  
  
## Syntax  
  
```  
  
Extract(Set_Expression, Hierarchy_Expression1 [,Hierarchy_Expression2, ...n] )  
```  
  
## Arguments  
 *Set_Expression*  
 A valid Multidimensional Expressions (MDX) expression that returns a set.  
  
 *Hierarchy_Expression1*  
 A valid Multidimensional Expressions (MDX) expression that returns a hierarchy.  
  
 *Hierarchy_Expression2*  
 A valid Multidimensional Expressions (MDX) expression that returns a hierarchy.  
  
## Remarks  
 The **Extract** function returns a set that consists of tuples from the extracted hierarchy elements. For each tuple in the specified set, the members of the specified hierarchies are extracted into new tuples in the result set. This function always removes duplicate tuples.  
  
 The **Extract** function performs the opposite action of the [Crossjoin](../mdx/crossjoin-mdx.md) function.  
  
## Examples  
 The following query shows how to use the **Extract** function on a set of tuples returned by the **NonEmpty** function:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `//Returns the distinct combinations of Customer and Date for all purchases`  
  
 `//of Bike Racks or Bike Stands`  
  
 `EXTRACT(`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `*`  
  
 `[Date].[Date].[Date].MEMBERS`  
  
 `*`  
  
 `{[Product].[Product Categories].[Subcategory].&[26],[Product].[Product Categories].[Subcategory].&[27]}`  
  
 `*`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `)`  
  
 `,  [Customer].[Customer], [Date].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
## See Also  
 [MDX Function Reference &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
