---
title: "Align the data in a paginated report chart in a table or matrix"
description: Discover uses for paginated report sparklines and data bars in Report Builder. These small, simple charts convey a lot of information with the minimum amount of detail.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/03/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Align the data in a paginated report chart in a table or matrix (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  Sparklines and data bars are small, simple charts that convey a lot of information with little extraneous detail in a paginated report. In a paginated report, when you check this option the values in your sparklines and data bars will align across the different cells in the table or matrix, even if there are missing values in the data they are based on.  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 In this image, the column chart shows daily sales for each employee. Note that for days that an employee has no sales, the chart leaves a blank and aligns subsequent days horizontally. It also aligns the charts vertically by making the sizes of the different charts relative to each other. For more information, see [Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## Align the data in a sparkline or data bar  
  
1.  [Add a sparkline or data bar](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) to a table or matrix.  
  
2. Click in the sparkline or data bar, and then click **Horizontal Axis Properties** or **Vertical Axis Properties**.  
  
2.  On the **Axis Options** tab, check the **Align axes in** box, and then in the dropdown box, select the group on which to align the axis.  
  
3.  Select **OK**.
  
## See Also  
 [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Add Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
