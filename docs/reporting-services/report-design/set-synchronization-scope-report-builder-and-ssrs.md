---
title: "Set synchronization scope in a paginated report"
description: Set synchronization scope in a paginated report with indicators to convey data values by synchronizing across the range of indicator values in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/07/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Set synchronization scope in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  In a paginated report, indicators convey data values by synchronizing across the range of indicator values within a specified scope.   
    
  By default, the scope is the parent container of the indicator such as the table or matrix that contains the indicator. You can change the synchronization of the indicator depending on the layout of your report. For example, if a data region such as a table has a row group, you can specify the group as the indicator scope. The indicator can also omit synchronization.  
  
 Options such as measurement units can be set by using expressions. For more information, see [Expressions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 For general information about understanding and setting scope within reports, see [Expression Scope for Totals, Aggregates, and Built-in Collections &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## To change the synchronization scope of an indicator  
  
1.  Right-click the indicator you want to change and click **Indicator Properties**.  
  
2.  Click **Values and States** in the left pane.  
  
3.  In the **Synchronization scope** list, click the scope that you want to apply.  
  
     The **(None)** option, which removes synchronization scope from the indicator, is always available. Other options depend on the layout of your report.  
  
     Optionally, click the **Expression** (*fx*) button to edit an expression that sets the scope.  
  
4.  Select **OK**.
  
## See Also  
 [Indicators &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
