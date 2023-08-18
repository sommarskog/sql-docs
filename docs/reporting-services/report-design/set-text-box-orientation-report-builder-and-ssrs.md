---
title: "Set text box orientation in a paginated report"
description: Find out how to rotate a text box in different directions in your paginated reports in Report Builder.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-design
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Set text box orientation in a paginated report (Report Builder)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-ssrs-rb](../../includes/ssrs-appliesto-ssrs-rb.md)] [!INCLUDE [ssrs-appliesto-pbi-rb](../../includes/ssrs-appliesto-pbi-rb.md)] [!INCLUDE [ssrb-applies-to-ssdt-yes](../../includes/ssrb-applies-to-ssdt-yes.md)]

In a paginated report, you can rotate a text box in different directions:   
* Horizontally   
* Vertically (rotated 90 degrees, with text reading from top to bottom, except East Asian text characters)

* Rotated by 270 degrees (text reading from bottom to top).   
  
Because you rotate the text box not the text, the rotation applies to all the text in the text box. You cannot specify different directions for parts of the text. Size the column width and the row height manually to accommodate the rotated text.  
  
 The WritingMode property, which you use to specify text orientation, isn't in the **Text Box Properties** dialog box. It's in the Properties pane and set the property there.   
  
## To rotate text  
  
1.  Create a report or open an existing report, and [add a text box](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md) to the design surface.  
  
3.  Select the text box that you want to rotate.  
  
2.  If the Properties pane is not open, on the **View** tab, select the **Properties** check box.  
  
4.  In the Properties pane, find the WritingMode property and select the text orientation to apply to the text box.  
  
    > [!NOTE]  
    >  When the properties in the Properties pane are organized into categories, WritingMode is in the **Localization** category.  
  
5.  In the list box, select **Horizontal**, **Vertical**, or **Rotate270**.  
  
## See Also  
 [Text Boxes &#40;Report Builder and SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Tutorial: Format Text &#40;Report Builder&#41;](../../reporting-services/tutorial-format-text-report-builder.md)  
  
  
