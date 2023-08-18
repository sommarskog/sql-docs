---
title: "Polar charts in a paginated report"
description: Discover the use of a paginated report polar chart with points grouped by category on a circle and values represented by the length of a point from the center of the circle.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/03/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Polar charts in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  A polar chart in a paginated report displays a series as a set of points that are grouped by category on a 360-degree circle. Values are represented by the length of the point as measured from the center of the circle. The farther the point is from the center, the greater its value. Category labels are displayed on the perimeter of the chart. For more information on how to add data to a polar chart, see [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Variations  
  
-   **Radar chart**. A radar chart displays a series as a circular line or area. Unlike the polar chart, the radar chart does not display data in terms of polar coordinates.  
  
## Data Considerations for Polar Charts  
  
-   The radar chart is useful for comparisons between multiple series of category data.  
  
-   Polar charts are most commonly used to graph polar data, where each data point is determined by an angle and a distance.  
  
-   Polar charts cannot be combined with any other chart type in the same chart area.  
  
## Example  
 The following example shows how a radar chart can be used. The table below provides sample data for the chart.  
  
|Name|Sales|  
|----------|-----------|  
|Shrubs|61|  
|Seeds|78|  
|Bulbs|60|  
|Trees|38|  
|Flowers|81|  
  
 In this example, the Name field is placed in the Category Groups area. The Sales field is placed in the Values area. The Sales field is automatically aggregated for the chart when you drop it. The radar chart calculates where to place the labels based on the number of values in the Sales field, which contains five values and places labels at five equidistant points on a circle. If the Sales field contained three values, the labels would be placed at three equidistant points on a circle.  
  
 The following illustration shows an example of a radar chart based on the data presented.  
  
 ![Radar chart](../../reporting-services/report-design/media/rs-radarchart.gif "Radar chart")  
  
## See Also  
 [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatting a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Chart Types &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Line Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)   
 [Empty and Null Data Points in Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
