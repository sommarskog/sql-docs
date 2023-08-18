---
title: "Add bevel, emboss, and texture styles to a paginated report chart"
description: Learn how to specify a drawing effect, such as bevels, embossing, or textures, to increase the visual impact of your paginated report chart in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Chart effects - add bevel, emboss, or texture to a paginated report chart (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  When using certain chart types in a paginated report, you can specify a drawing effect to increase the visual impact of your chart. These drawing effects are only applied to the series of your chart. They have no effect on any other chart element.  
  
 When you are using any variant of a pie or doughnut chart, you can specify a soft edge or concave drawing style, similar to bevel or emboss effects that can be applied to an image.  
  
 When you are using any variant of a bar or column chart, you can apply texture styles, such as cylinder, wedge, and light-to-dark, to the individual bars or columns.  
  
 In addition to these drawing styles, you can add borders and shadows to many chart elements to give the illusion of depth. For more information on other ways to format the chart, see [Formatting a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### To add bevel or emboss styles to a pie or doughnut chart  
  
1.  On the **View** tab, select **Properties** to open the Properties pane.  
  
2.  Select the pie or doughnut chart that you want to enhance. Select a data field in the chart, not the entire chart.  
  
3.  In the Properties pane, expand the **CustomAttributes** node.  
  
4.  For PieDrawingStyle, select a style from the drop-down list.  
  
> [!NOTE]  
>  You can't have 3D and bevel or emboss styles on the same chart. If you have enabled 3D for the chart, you will not see the PieDrawingStyle property.  
  
 ![Pie chart with concave drawing style](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "Pie chart with concave drawing style")  
  
### To add texture styles to a bar or column chart  
  
1.  Select the bar or column chart that you want to enhance. Select a data field in the chart, not the entire chart.  
  
2.  Open the Properties pane.  
  
3.  Expand the **CustomAttributes** node.  
  
4.  For DrawingStyle, select a style from the drop-down list.  
  
> [!NOTE]  
>  You can't have 3D and bevel or emboss styles on the same chart. If you have enabled 3D for the chart, you will not see the PieDrawingStyle property.  
  
 ![Bar chart with LightToDark drawing effect](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "Bar chart with LightToDark drawing effect")  
  
## See Also  
 [Bar Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [Column Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [Pie Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [Formatting a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
