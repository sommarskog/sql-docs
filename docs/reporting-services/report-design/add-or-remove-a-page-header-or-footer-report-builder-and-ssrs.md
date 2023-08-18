---
title: "Add or remove a page header or footer in a paginated report"
description: Find out how you can add static text, images, lines, rectangles, and borders to paginated report page headers or footers in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Add or remove a page header or footer in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

  You can add static text, images, lines, rectangles, and borders to paginated report page headers or footers. You can place expressions and data-bound images in a textbox if you want variable or computed data in a header or footer.  
  
> [!NOTE]  
>  Each rendering extension processes page headers and footers differently. For more information, see [Page Headers and Footers &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md) and [Pagination in Reporting Services &#40;Report Builder  and SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### To add a page header or footer  
  
1.  Open a report.  
  
2.  On the design surface, right-click the report, point to **Insert**, and then click **Header** or **Footer**.  
  
> [!NOTE]  
>  The **Header** and **Footer** options appear only when a header or footer is not already part of the report.  
  
### To configure a page header or footer  
  
1.  On the design surface, right-click the page header or footer.  
  
2.  Point to **Insert**, and then click one of the following items to add it to the header or footer area:  
  
    -   **Textbox**  
  
    -   **Line**  
  
    -   **Rectangle**  
  
    -   **Image**  
  
3.  Right-click the page header, and then click **Header Properties** to add borders, background images, or colors, or to adjust the width of the header. Then click **OK**.  
  
4.  Right-click the page footer, and then click **Footer Properties** to add borders, background images, or colors, or to adjust the width of the footer. Then click **OK**.  
  
### To remove a page header or footer  
  
1.  Open a report.  
  
2.  On the design surface, right-click the page header or footer, and then click **Delete**.  
  
> [!NOTE]  
>  When you remove a page header or footer, you delete it from the report. Any items that you previously added to the page header or footer will not reappear if you subsequently add the header or footer again.  
  
## See Also  
 [Page Headers and Footers &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
  
  
