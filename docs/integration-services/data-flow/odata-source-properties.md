---
title: "OData Source Properties"
description: "OData Source Properties"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# OData Source Properties

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


When you right-click **OData Source** in the data flow and click **Properties**, you see properties for the **OData Source** component in the **Properties** window.  

## Properties 

|Property|Description|  
|-|-|  
|CollectionName|Name of the collection to retrieve from the OData service. The **CollectionName** property is used when **UseResourcePath** is False.<br /><br /> This property is expressionable, which lets you set the value at runtime. However, if the metadata of the collection does not match the metadata that existed at design time, a validation error occurs, causing the data flow execution to fail.|  
|DefaultStringLength|This value specifies default length for string columns that have no max length.<br /><br /> **Default:** 4000|  
|Query|The OData query parameters. This property is expressionable and can be set at runtime.|  
|ResourcePath|Use this property when you need to specify a full resource path, rather than selecting a collection name. This property is used when **UseResourcePath** is True.|  
|UseResourcePath|When set to True, the **ResourcePath** value is appended to the base URL to determine the OData feed location. When set to False, the **CollectionName** value is used.<br /><br /> **Default:** False|  
  
## See Also
[OData Source](odata-source.md)
