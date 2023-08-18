---
title: Derived Hierarchies with Explicit Caps
description: "Derived Hierarchies with Explicit Caps (Master Data Services)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
helpviewer_keywords:
  - "hierarchies [Master Data Services], derived hierarchies with explicit caps"
  - "explicit hierarchies, derived hierarchies with explicit caps"
  - "derived hierarchies, derived hierarchies with explicit caps"
---
# Derived Hierarchies with Explicit Caps (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], when the levels from an explicit hierarchy are used as the top levels of a derived hierarchy, this is called a derived hierarchy with an explicit cap.  
  
 The explicit hierarchy must be based on the same entity as the entity at the top of the derived hierarchy.  
  
 In the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] user interface (UI), you create this type of hierarchy by dragging an explicit hierarchy to the top of a derived hierarchy.  
  
 ![mds_conc_explicit_cap_UI_structure](../master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## Derived Hierarchy with Explicit Cap Example  
 In this example, the members in the explicit hierarchy are from the Subcategory entity. In the derived hierarchy, the top-level members are also from the Subcategory entity.  
  
 ![mds_conc_explicit_cap_UI_example](../master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 By using the explicit hierarchy at the top of a derived hierarchy, the derived hierarchy becomes ragged.  
  
## Rules  
  
-   You cannot have more than one explicit hierarchy in a derived hierarchy with explicit cap.  
  
-   You can use the same explicit hierarchy as a cap for multiple derived hierarchies.  
  
-   You cannot assign hierarchy member permissions to derived hierarchies with explicit caps. If you assign permissions to either the explicit hierarchy or the derived hierarchy individually, the permissions affect both hierarchies.  
  
## Related Tasks  
  
|Task Description|Topic|  
|----------------------|-----------|  
|Create a derived hierarchy.|[Create a Derived Hierarchy &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Create an explicit hierarchy.|[Create an Explicit Hierarchy &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Delete an existing derived hierarchy.|[Delete a Derived Hierarchy &#40;Master Data Services&#41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## Related Content  
  
-   [Derived Hierarchies &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Explicit Hierarchies &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
