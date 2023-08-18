---
title: "Add an expression to a paginated report"
description: Find out about how to use expressions to define report item properties, filters, and parameter values in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Add an expression to a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  Expressions are used throughout paginated reports for defining report item properties, filters, groups, sort order, connection strings, and parameter values. Expressions begin with an equal sign (=) and are written in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. They are evaluated at run time by the report processor, which combines the evaluation result with report layout elements.  
  
 Expressions can be simple or complex. Simple expression refer to a single item in a built-in collection. Complex expressions can contain constants, operators, global collection items, and function calls. For more information, see [Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### To add an expression to a text box  
  
-   In **Design** view, click the text box on the design surface to which you want to add an expression.  
  
    -   For a simple expression, type the display text for the expression in the text box. For example, for the dataset field Sales, type `[Sales]`.  
  
    -   For a complex expression, right-click the text box, and select **Expression**. The **Expression** dialog box opens. Type or interactively create your expression after the '=' in the expression pane, and then click OK.  
  
         The expression appears on the design surface as `<<Expr>>`.  
  
## See Also  
 [Formatting Text and Placeholders &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Text Boxes &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Expression Uses in Reports &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Filter Equation Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Group Expression Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Expression Dialog Box &#40;Report Builder&#41;](./expressions-report-builder-and-ssrs.md)   
 [Expression Examples &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Add Code to a Report &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)  
  
