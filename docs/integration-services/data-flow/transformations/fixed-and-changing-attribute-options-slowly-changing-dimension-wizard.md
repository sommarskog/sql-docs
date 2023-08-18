---
title: "Fixed and Changing Attribute Options (Slowly Changing Dimension Wizard"
description: "Fixed and Changing Attribute Options (Slowly Changing Dimension Wizard"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.loaddimwizard.attriboption.f1"
---
# Fixed and Changing Attribute Options (Slowly Changing Dimension Wizard

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Use the **Fixed and Changing Attribute Options** dialog box to specify how to respond to changes in fixed and changing attributes.  
  
 To learn more about this wizard, see [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## Options  
 **Fixed attributes**  
 For fixed attributes, indicate whether the task should fail if a change is detected in a fixed attribute.  
  
 **Changing attributes**  
 For changing attributes, indicate whether the task should change outdated or expired records, in addition to current records, when a change is detected in a changing attribute. An expired record is a record that has been replaced with a newer record by a change in a historical attribute (a Type 2 change). Selecting this option may impose additional processing requirements on a multidimensional object constructed on the relational data warehouse.  
  
## See Also  
 [Configure Outputs Using the Slowly Changing Dimension Wizard](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
