---
title: Navigational Access
description: "Navigational Access (Master Data Services)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
helpviewer_keywords:
  - "navigational access [Master Data Services]"
  - "security [Master Data Services], navigational access"
---
# Navigational Access (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Navigational access applies to model object security, which is assigned on the **Models** tab.  
  
 Navigational access is the access you get to levels higher than where you've assigned security.  
  
 In this example, permissions are assigned to an entity, and so navigational access is granted at the model level.  
  
 ![mds_conc_inheritance_model](../master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **Entities**  
  
 When you assign permission to an entity, its leaf members, or its consolidated members, navigational access means you can read or update the name and code for all members. You can also read the model name.  
  
 **Attributes**  
  
 When you assign permission to an attribute, navigational access means you can read or update the name and code for all members in the entity. You can also read the model name.  
  
 **Collections**  
  
 When you assign permissions to collections, you can read or update the name, code, description and owner ID. You can also read the model name.  
  
## See Also  
 [How Permissions Are Determined &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
