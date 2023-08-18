---
title: "Template Caching (SQLXML)"
description: Learn how to significantly improve performance when executing templates by using template caching in SQLXML 4.0.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "reference"
helpviewer_keywords:
  - "registry keys [SQLXML]"
  - "cache [SQLXML]"
  - "templates [SQLXML], caching"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Template Caching (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Template caching significantly improves performance. If template caching is set, the template remains in memory upon its first execution. This improves the performance for the subsequent execution of the template.  
  
 You can set the template cache size by adding the following key in the registry:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 The template size should be set on the basis of the available memory and the number of templates you are using. The default of **TemplateCacheSize** size is 31. You can increase the cache size if template access seems slow, or decrease the cache size if memory is low.  
  
 For better performance, it is recommended that you set **TemplateCacheSize** higher than the number of templates you usually use. If **TemlateCacheSize** is less than the number of templates you have, performance degrades as the number of templates increase. The **TemplateCacheSize** can be set to a maximum of 128.  
  
 Every time a cached template is used, the modification time of the template file is checked to see whether it needs to be refreshed. This is because the disk copy is newer than the cache copy.  
  
> [!NOTE]  
>  Template parameters and command properties are not cached.  
  
## See Also  
 [Schema Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [XSL Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
