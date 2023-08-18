---
title: "XSL Caching (SQLXML)"
description: Learn how to cache XSL style sheets and set the XSL cache size to improve query performance in SQLXML 4.0.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "reference"
helpviewer_keywords:
  - "registry keys [SQLXML]"
  - "cache [SQLXML]"
  - "XSL caching [SQLXML]"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# XSL Caching (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Caching XSL style sheets improves performance. Upon its first execution, an XSL style sheet remains in memory if XSL caching is set to ON; this improves performance for subsequent processing. The default setting is ON.  
  
 You can set the XSL cache size by adding the following key in the registry:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 The XSL cache size should be set on the basis of the available memory and the number of XSL style sheets you are using. The default of **XSLCacheSize** size is 31. You can increase the cache size if XSL access seems slow, or decrease the cache size if memory is low.  
  
 For better performance, it is recommended that you set **XSLCacheSize** higher than the number of XSL style sheets you usually use. If **XSLCacheSize** is less than the number of XSL style sheets you have, the performance degrades as the number of XSL style sheets increases. The **XSLCacheSize** can be set to a maximum of 128.  
  
 Every time the cached XSL style sheet is used, the modification time of the XSL file is checked to determine whether it needs to be refreshed. This is because the disk copy is newer than the cache copy.  
  
## See Also  
 [Template Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Schema Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
