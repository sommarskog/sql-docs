---
title: "Print Reports"
description: You can view and print a report from the web portal or an application that you use to view it. The client computer performs print processing on demand.
author: maggiesMSFT
ms.author: maggies
ms.date: 05/24/2018
ms.service: reporting-services
ms.subservice: report-builder
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Print Reports - Reporting Services (SSRS)

  After you save a report to a report server, you can view and print the report from the web portal or any application that you use to view an exported report. Before saving a report, you can print it when you preview it.

All print processing is performed on demand and on the client computer. There is no server-side print functionality that enables you to route a print job directly from a report server to a printer that is attached to the Web server. Printers and print options are selected by individual report users by using a standard **Print** dialog box.

Report authors who design reports specifically for print output can use page breaks, page headers and footers, expressions, and background images to create a print-based design. Examples of report design elements intended for print output might include terms and conditions that you print on the back of every report, or graphic and text elements that mimic letterhead.

Due to the way pagination is implemented for different rendering formats, you might not be able to achieve optimum print output results for every report in every rendering format. The following list provides examples:

1. Report pages are designed to accommodate variable amounts of data. Reports that include a matrix, for example, can cause a page to grow both horizontally and vertically depending on whether a user interactively toggles rows and columns. A user who does not expand a matrix will get different print results than a user who does.

1. You cannot combine landscape and portrait mode pages in the same report, nor is there a way to create a print-based layout that replaces or exists alongside the layout of a report as rendered in a browser or other application.

1. For most exported reports, report printouts include everything that is visible on the report, as viewed by the user on a computer monitor. White space from the report design surface is preserved. To add or remove extra blank pages horizontally, change the report page width.

> [!NOTE]  
> HTML report printouts may contain only the content on the first page if you are using the browser's Print command. You can achieve better results if you print HTML reports using the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] client printing functionality. For more information, see [Print Reports from a Browser with the Print Control (Report Builder and SSRS)](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md).

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## In This Section

[Print Reports from a Browser with the Print Control (Report Builder and SSRS)](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
Describes how to use client-side printing to print reports from the web portal.

[Print Reports from Other Applications (Report Builder and SSRS)](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
Describes how to print reports exported to another application.

[Print a Report (Report Builder and SSRS)](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
Provides step-by-step instructions on how to print a report, how to control the margins on a page, and on how to specify the paper size for reports that will be rendered by hard-page break renderers: PDF, Image, or Print.

## See also

- [Export Reports (Report Builder and SSRS)](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)
- [Page Headers and Footers (Report Builder and SSRS)](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)
- [Images (Report Builder and SSRS)](../../reporting-services/report-design/images-report-builder-and-ssrs.md)
- [Pagination in Reporting Services (Report Builder  and SSRS)](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)
