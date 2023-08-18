---
title: "Apply Data Quality Rules to Data Source"
description: "Apply Data Quality Rules to Data Source"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# Apply Data Quality Rules to Data Source

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  You can use Data Quality Services (DQS) to correct data in the package data flow by connecting the DQS Cleansing transformation to the data source. For more information about DQS, see [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). For more information about the transformation, see [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 When you process data with the DQS Cleansing transformation, a data quality project is created on the Data Quality Server. You use the Data Quality Client to manage the project. For more information, see [Open, Unlock, Rename, and Delete a Data Quality Project](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md).  
  
### To correct data in the data flow  
  
1.  Create a package.  
  
2.  Add and configure the DQS Cleansing transformation. For more information, see [DQS Cleansing Transformation Editor Dialog Box](./dqs-cleansing-transformation.md).  
  
3.  Connect the DQS Cleansing transformation to a data source.  
  
