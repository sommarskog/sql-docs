---
title: "Schema Caching (SQLXML)"
description: Learn how to use registry keys to explicitly control schema caching and improve the performance of an XPath query in SQLXML 4.0.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "reference"
helpviewer_keywords:
  - "registry keys [SQLXML]"
  - "cache [SQLXML]"
  - "schemas [SQLXML]"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Schema Caching (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  With a side-by-side installation of XML for Microsoft SQL Server 2000 Web Release 1, Microsoft SQLXML 2.0, and SQLXML 3.0, you can explicitly control the schema caching in all versions by using the following registry keys:  
  
 Web Release 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 For more information about side-by-side installation, see [What's New in SQLXML 4.0 SP1](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 Schema caching significantly improves the performance of an XPath query. When an XPath query is executed against a mapping schema, the schema is stored in memory, and the necessary data structures are built in memory. If schema caching is set, the schema remains in memory, thereby improving performance for subsequent XPath queries.  
  
 You can set the schema cache size by adding the above key in the registry  
  
 The schema size is set based on the available memory and the number of schemas you are using. The default **SchemaCacheSize** size is 31. If you set **SchemaCacheSize** higher, more memory is used. Therefore, you can increase the cache size if schema access seems slow, or decrease the cache size if memory is low.  
  
 For performance reasons, it is recommended that you set **SchemaCacheSize** higher than the number of mapping schemas you usually use. As the number of schemas increase, if **SchemaCacheSize** is less than the number of schemas you have, the performance degrades.  
  
> [!NOTE]  
>  During development, it is recommended that you do not cache the schemas, because the changes to the schemas are not reflected in the cache for about two minutes.  
  
## See Also  
 [Template Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [XSL Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
