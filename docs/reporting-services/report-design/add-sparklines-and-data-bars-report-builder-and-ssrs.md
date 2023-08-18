---
title: "Add sparklines and data bars in a paginated report"
description: "Add sparklines and data bars in a paginated report."
author: maggiesMSFT
ms.author: maggies
ms.date: 03/03/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Add sparklines and data bars in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  Sparklines and data bars are small, spare charts that convey a lot of information with little extraneous detail in a paginated report. For more information about them, see [Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
 In paginated reports, sparklines and data bars are most commonly placed in cells in a table or matrix. Sparklines usually display only one series each. Data bars can contain one or more data points. Both sparklines and data bars derive their impact from repeating the series information for each row in the table or matrix.  
  
## To add a sparkline or data bar to a table or matrix  
  
1.  If you have not done so already, create a [table](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) or [matrix](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md) with the data you want to display.  
  
2.  Insert a column in your table or matrix. For more information, see [Insert or Delete a Column &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  On the **Insert** tab, click **Sparkline** or **Data Bar**, and then click in a cell in the new column.  
  
    > [!NOTE]  
    >  You cannot place sparklines in a detail group in a table. They must go in a cell associated with a group.  
  
4.  In the **Change Sparkline/Data Bar Type** dialog box, click the kind of sparkline or data bar you want, and then click **OK**.  
  
5.  Click the sparkline or data bar.  
  
     The **Chart Data** pane opens.  
  
6.  In the **Values** area, click the **Add Fields** plus sign (**+**), and then click the field whose values you want charted.  
  
7.  In the **Category Groups** area, click the **Add Fields** plus sign (**+**), and then click the field whose values you want to group by.  
  
     Typically for sparklines and data bars, you will not add a field to the **Series Group** area because you only want one series for each row.  
  
## See Also  
 [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Align the Data in a Chart in a Table or Matrix &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
