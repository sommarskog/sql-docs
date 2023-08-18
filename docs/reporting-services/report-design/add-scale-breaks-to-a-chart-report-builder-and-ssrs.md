---
title: "Add scale breaks to a paginated report chart"
description: Find out about using a scale break to display two distinct ranges in the same paginated report chart area in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 05/30/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---

# Add scale breaks to a paginated report chart (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  A scale break is a stripe drawn across the plotting area of a chart to denote a break in continuity between the high and low values on a value axis (usually the vertical, or y-axis). Use a scale break to display two distinct ranges in the same chart area in a paginated report.  
  
 ![Chart with scale break](../../reporting-services/report-design/media/rs-multipledatarangeschart-scalebreak.gif "Chart with scale break")  
  
> [!NOTE]  
>  You cannot specify where to place a scale break on your chart. The chart uses its own calculations based on the values in your dataset to determine whether there is sufficient separation between data ranges to draw a scale break on the value axis (y-axis) at run time.  
  
 An example of a chart with scale breaks is available as a sample report. For more information about downloading this sample report and others, see [Report Builder and Report Designer sample reports](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### To enable scale breaks on the chart  
  
1.  Right-click the vertical axis and then click **Axis Properties**. The **VerticalAxis Properties** dialog box opens.  
  
2.  Select the **Enable scale breaks** check box.  
  
### To change the style of the scale break  
  
1.  Open the Properties pane.  
  
2.  On the design surface, right-click on the y-axis of the chart. The properties for the y-axis object (named Chart Axis by default) are displayed in the Properties pane.  
  
3.  In the **Scale** section, expand the ScaleBreakStyle property.  
  
4.  Change the values for ScaleBreakStyle properties, such as BreakLineType and Spacing. For more information about scale break properties, see [Displaying a Series with Multiple Data Ranges on a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/displaying-a-series-with-multiple-data-ranges-on-a-chart.md).  

## Next steps

[Charts](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[Formatting a Chart](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[Axis Properties Dialog Box, Axis Options](/previous-versions/sql/)  

More questions? [Try asking the Reporting Services forum](https://go.microsoft.com/fwlink/?LinkId=620231)
