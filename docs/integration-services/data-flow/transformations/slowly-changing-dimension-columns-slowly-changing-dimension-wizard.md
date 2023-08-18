---
title: "Slowly Changing Dimension Columns (Slowly Changing Dimension Wizard)"
description: "Slowly Changing Dimension Columns (Slowly Changing Dimension Wizard)"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.loaddimwizard.scdsupport.f1"
---
# Slowly Changing Dimension Columns (Slowly Changing Dimension Wizard)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Use the **Slowly Changing Dimensions Columns** dialog box to select a change type for each slowly changing dimension column.  
  
 To learn more about this wizard, see [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## Options  
 **Dimension Columns**  
 Select a dimension column from the list.  
  
 **Change Type**  
 Select a **Fixed Attribute**, or select one of the two types of changing attributes. Use **Fixed Attribute** when the value in a column should not change; [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] then treats changes as errors. Use **Changing Attribute** to overwrite existing values with changed values. Use **Historical Attribute** to save changed values in new records, while marking previous records as outdated.  
  
 **Remove**  
 Select a dimension column, and remove it from the list of mapped columns by clicking **Remove**.  
  
## See Also  
 [Configure Outputs Using the Slowly Changing Dimension Wizard](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
