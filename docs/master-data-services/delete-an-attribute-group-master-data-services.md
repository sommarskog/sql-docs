---
title: Delete an Attribute Group
description: "Delete an Attribute Group (Master Data Services)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
helpviewer_keywords:
  - "deleting attribute groups [Master Data Services]"
  - "attribute groups [Master Data Services], deleting"
---
# Delete an Attribute Group (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], delete an attribute group when you no longer need the tab to display in the **Explorer** functional area of [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   **Note** When attribute groups exist, attributes that do not belong to an attribute group are not displayed in **Explorer**. When no attribute groups exist, all attributes are displayed.  
  
## Prerequisites  
 To perform this procedure:  
  
-   You must have permission to access the **System Administration** functional area.  
  
-   You must be a model administrator. For more information, see [Administrators &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### To delete an attribute group  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], click **System Administration**.  
  
2.  On the **Manage Model** page, select a model from the grid and then click **Entities**.  
  
3.  On the **Manage Entity** page, from the grid, select the row for the entity that you want to edit an attribute group.  
  
4.  Click **Attribute Groups**.  
  
5.  On the **Manage Attribute Groups** page, select member type from the **Member Types** drop-down list to expand **Leaf**, **Consolidated**, or **Collection**, depending on the type of group you want to delete.  
  
6.  Click the attribute group you want to delete.  
  
7.  Click **Delete**.  
  
8.  In the confirmation dialog box, click **OK**.  
  
## See Also  
 [Attribute Groups &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Create an Attribute Group &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
