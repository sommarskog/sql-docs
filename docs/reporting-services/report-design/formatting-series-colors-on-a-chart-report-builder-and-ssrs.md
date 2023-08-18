---
title: "Formatting series colors on a paginated report chart"
description: Learn how to use the many built-in palettes in paginated reports for charts or define a custom palette of your own design in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/03/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "10245"
  - "10252"
  - "sql13.rtp.rptdesigner.serieslabelproperties.borders.f1"
  - "sql13.rtp.rptdesigner.seriesproperties.borders.f1"
---
# Formatting series colors on a paginated report chart (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

Report Builder provides several built-in palettes for paginated report charts, or you can define a custom palette. By default, charts use the built-in **Pacific** color palette to fill each series. These colors also appear in the legend. When multiple series are added to the chart, the chart assigns the series a color in the order that the colors have been defined in the palette.  
  
 If there are a greater number of series than there are colors in the palette, the chart will begin reusing colors, and two series may have the same color. This frequently occurs if you are using a Shape chart, where each data point is assigned a color from the palette. To avoid confusion, define a custom palette with at least the same number of colors as you have series on your chart.  
  
 You can select a new palette or define a custom palette from the Properties pane. For more information, see [Define Colors on a Chart Using a Palette &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Using Built-In Palettes  
 Reporting Services provides a list of predefined, built-in palettes that you can use to define a color set for series on your chart. All built-in palettes contain between 10 and 16 color values. You cannot extend the built-in palette to include more colors, so if you need more than 16 colors, you must define a custom palette.  
  
 If you are printing a report, consider using the **Greyscale** palette. This palette uses shades of black and white to represent each series in a chart.  
  
 The palette named Default was used as the default chart palette in earlier versions of Reporting Services. It has been maintained with the same name for consistency. Charts will upgrade seamlessly using the Default palette, but after upgrading, you might consider changing it.  
  
## Using Custom Palettes  
 If you want to apply your own colors to the chart, use a custom palette. A custom palette let you add your own colors in the order you want them to appear on the chart. A custom palette is especially helpful if the number of series in your chart is unknown at design time. For more information, see [Define Colors on a Chart Using a Palette &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md).  
  
## Using a Color Fill on Each Series  
 You can also define your own colors on the chart by specifying a color for each series on the chart. To do this, open the **Series Properties** dialog box and set the **Color** property for **Fill**. This approach will override all defined palettes. Generally, it is better to use a custom palette to define your own colors because the number of series in your dataset may not be known until report processing.  
  
 This approach is best suited when you want to conditionally set the color of the series based on an expression.  For more information, see [Formatting Data Points on a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md).  
  
## In This Section  
 [Specify Consistent Colors across Multiple Shape Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
 [Define Colors on a Chart Using a Palette &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md))  
  
 [Highlight Chart Data by Adding Strip Lines &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs.md)  
  
## See Also  
 [Formatting a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Add Bevel, Emboss, and Texture Styles to a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [Charts &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Formatting the Legend on a Chart &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/chart-legend-formatting-report-builder.md)  
  
  
