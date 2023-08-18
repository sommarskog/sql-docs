---
title: "Azure Data Lake Store Destination"
description: "Azure Data Lake Store Destination"
author: chugugrace
ms.author: chugu
ms.date: 05/22/2019
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "SQL13.DTS.DESIGNER.AFPADLSDEST.F1"
  - "sql14.dts.designer.afpadlsdest.f1"
---
# Azure Data Lake Store Destination

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  The **Azure Data Lake Store Destination** component enables an SSIS package to write data to an Azure Data Lake Store. The supported file formats are: Text, Avro, and ORC. 
  
 The **Azure Data Lake Store Destination** is a component of the [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
> [!NOTE]
> To ensure that the Azure Data Lake Store Connection Manager and the components that use it - that is, the Azure Data Lake Store Source and the Azure Data Lake Store Destination - can connect to services, make sure you download the latest version of the Azure Feature Pack [here](https://www.microsoft.com/download/details.aspx?id=49492). 

**Configure the Azure Data Lake Store Destination**

1. Drag-drop **Azure Data Lake Store Destination** to the data flow designer and double-click it to see the editor.  

2.  For the **Azure Data Lake Store connection manager** field, specify an existing Azure Data Lake Store Connection Manager or create a new one that refers to an Azure Data Lake Store service.  
  
    1.  For the **File Path** field, specify the file name you want to write data to. If this file already exists, its contents are overwritten.  
  
    2.  For the **File format** field, specify the file format you want to use.  
  
       If the file format is Text, you must specify the **Column delimiter character** value. Also  select **Column names in the first data row** if the first row in the file contains column names.  

       If the file format is ORC, Java is required. See [here](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java) for details.
  
3.  After specifying the connection information, switch to the **Columns** page to map source columns to destination columns for the SSIS data flow.  
