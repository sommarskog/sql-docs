---
title: "Formatting ranges on a gauge in a paginated report"
description: Visually indicate with a gauge range in a paginated report when the pointer value has gone into a certain span of values in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Formatting ranges on a gauge in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

 In a paginated report, the gauge range is a zone or area on the gauge scale that indicates an important subsection of values on the gauge. Using a gauge range, you can visually indicate when the pointer value has gone into a certain span of values. Ranges are defined by a start value and an end value.  
  
 You can also use ranges to define different sections of a gauge. For example, on a gauge with values from 0 to 10, you can define a red range that has a value from 0 to 3, a yellow range that has a value from 4 to 7 and a green range that has a value from 8 to 10. If the start value that you specified is greater than the end value that you specified, the values are swapped so that the start value is the end value and the end value is the start value.  
  
 You can position the range in the same way that you position pointers on a scale. The **Position** and **Distance from scale** properties determine the position of the range. For more information, see [Gauges &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## See Also  
 [Formatting Scales on a Gauge &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatting Pointers on a Gauge &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Set a Minimum or Maximum on a Gauge &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)   
 [Tutorial: Adding a KPI to Your Report &#40;Report Builder&#41;](../../reporting-services/tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [Gauges &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
