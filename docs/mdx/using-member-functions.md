---
title: "Using Member Functions"
description: "Using Member Functions"
author: minewiskan
ms.author: owend
ms.reviewer: owend
ms.date: 02/17/2022
ms.service: sql
ms.subservice: analysis-services
ms.topic: reference
ms.custom: mdx
---
# Using Member Functions


  A member function is an Multidimensional Expressions (MDX) function that returns a member. Member functions, like tuple functions and set functions, are essential to negotiating the multidimensional structures found in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Of the many member functions in MDX, the most important is the **CurrentMember** function, which is used to determine the current member on a hierarchy. The following query illustrates how to use it, along with the **Parent**, **Ancestor**, and **Prevmember** functions:  
  
 `WITH`  
  
 `//Returns the name of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[CurrentMemberDemo] AS [Date].[Calendar].CurrentMember.Name`  
  
 `//Returns the name of the parent of the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[ParentDemo] AS [Date].[Calendar].CurrentMember.Parent.Name`  
  
 `//Returns the name of the ancestor of the currentmember on the Calendar hierarchy at the Year level`  
  
 `MEMBER MEASURES.[AncestorDemo] AS ANCESTOR([Date].[Calendar].CurrentMember, [Date].[Calendar].[Calendar Year]).Name`  
  
 `//Returns the name of the member before the currentmember on the Calendar hierarchy`  
  
 `MEMBER MEASURES.[PrevMemberDemo] AS [Date].[Calendar].CurrentMember.Prevmember.Name`  
  
 `SELECT{MEASURES.[CurrentMemberDemo],MEASURES.[ParentDemo],MEASURES.[AncestorDemo],MEASURES.[PrevMemberDemo] } ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## See Also  
 [Functions &#40;MDX Syntax&#41;](../mdx/functions-mdx-syntax.md)   
 [Using Tuple Functions](../mdx/using-tuple-functions.md)   
 [Using Set Functions](../mdx/using-set-functions.md)  
  
  
