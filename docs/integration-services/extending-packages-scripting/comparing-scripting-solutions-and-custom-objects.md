---
title: "Comparing Scripting Solutions and Custom Objects"
description: "Comparing Scripting Solutions and Custom Objects"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "reference"
helpviewer_keywords:
  - "managed tasks [Integration Services]"
  - "Script task [Integration Services], vs. custom managed tasks"
  - "SSIS Script task, vs. custom managed tasks"
  - "custom tasks [Integration Services], scripts"
dev_langs:
  - "VB"
---
# Comparing Scripting Solutions and Custom Objects

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  An [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Script task or Script component can implement much of the same functionality that is possible in a custom managed task or data flow component. Here are some considerations to help you choose the appropriate type of task for your needs:  
  
-   If the configuration or functionality is specific to an individual package, you should use the Script task or the Script component instead of a developing a custom object.  
  
-   If the functionality is generic, and might be used in the future for other packages and by other developers, you should create a custom object instead of using a scripting solution. You can use a custom object in any package, whereas a script can be used only in the package for which it was created.  
  
-   If the code will be reused within the same package, you should consider creating a custom object. Copying code from one Script task or component to another leads to reduced maintainability by making it more difficult to maintain and update multiple copies of the code.  
  
-   If the implementation will change over time, consider using a custom object. Custom objects can be developed and deployed separately from the parent package, whereas an update made to a scripting solution requires the redeployment of the whole package.  
  
## See Also  
 [Extending Packages with Custom Objects](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
