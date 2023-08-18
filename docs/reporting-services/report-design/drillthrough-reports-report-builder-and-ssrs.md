---
title: "Drillthrough reports in a paginated report"
description: Discover drillthrough reports, which open when you select a link in a paginated report to get details about an item in an original summary report in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/07/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Drillthrough reports in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-not-pbi-rb](../../includes/ssrs-appliesto-not-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  A drillthrough report is a report that a user opens by clicking a link within another paginated report. Drillthrough reports commonly contain details about an item that is contained in an original summary report. For example, in this illustration, the sales summary report lists sales orders and totals. When a user clicks an order number in the summary list, another report opens that contains details about the order.  
  
 ![rs_DrillThru](../../reporting-services/report-design/media/rs-drillthru.gif "rs_DrillThru")  
  
 The data in the drillthrough report is not retrieved until the user clicks the link in the main report that opens the drillthrough report. If the data for the main report and the drillthrough report must be retrieved at the same time, consider using a subreport. For more information, see [Subreports &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  When you are working in Report Builder, you must be connected to a report server to view the drillthrough report that opens when you click the drillthrough link in the main report.  
  
 To get started quickly with drillthrough reports, see [Tutorial: Creating Drillthrough and Main Reports &#40;Report Builder&#41;](../../reporting-services/tutorial-creating-drillthrough-and-main-reports-report-builder.md). 
   
## Parameters in Drillthrough Reports  
 A drillthrough report typically contains parameters that are passed to it by the summary report. In the sales summary report example, the summary report includes the field [OrderNumber] in a text box in a table cell. The drillthrough report contains a parameter that takes the order number as a value. When you set the drillthrough report link on the text box for [OrderNumber], you also set the parameter for the target report to [OrderNumber]. When the user clicks the order number in the summary report, the target detail report opens and displays the information for that order number. To view instructions about customizing drillthrough reports based on parameter values, see [Report Parameters &#40;Report Builder and Report Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md) and the [InScope Function &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/report-builder-functions-inscope-function.md).  
  
## Designing the Drillthrough Report  
 To create a drillthrough report, you must design the drillthrough report first, before you create the drillthrough action in the main report.  
  
 A drillthrough report can be any report. Typically, the drillthrough report accepts one or more parameters to specify the data to show, based on the link from the main report. For example, if the link from the main report was defined for a sales order, then the sales order number is passed to the drillthrough report.  
  
## Creating a Drillthrough Action in the Main Report  
 You can add drillthrough links to text boxes (including text in the cells of a table or matrix), images, charts, gauges, and any other report item that has an Action property page. For more information, see [Add a Drillthrough Action on a Report &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
 You can create the drillthrough action in the main report as a report action or a URL action. For a report action, the drillthrough report must exist on the same report server as the main report. For a URL action, the report must exist at the fully qualified URL location. The way that you specify a report might differ for a report server or a SharePoint site that is integrated with a report server. If the report server is configured in SharePoint integrated mode, only URL actions are supported.  
  
 For more information, see [Add a Drillthrough Action on a Report &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) and [Specifying Paths to External Items &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
## Viewing a Drillthrough Report  
 To view a summary report with drillthrough links after it is published, you must ensure that the drillthrough reports reside on the same report server as the summary report. In all cases, the user must have permissions on the drillthrough report to view it.  
  
## See Also  
 [Drillthrough, Drilldown, Subreports, and Nested Data Regions &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  
