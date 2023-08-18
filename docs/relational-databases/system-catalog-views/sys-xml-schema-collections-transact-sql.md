---
title: "sys.xml_schema_collections (Transact-SQL)"
description: sys.xml_schema_collections (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: mikeray
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.xml_schema_collections_TSQL"
  - "sys.xml_schema_collections"
  - "xml_schema_collections"
  - "xml_schema_collections_TSQL"
helpviewer_keywords:
  - "sys.xml_schema_collections catalog view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.xml_schema_collections (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns a row per XML schema collection. An XML schema collection is a named set of XSD definitions. The XML schema collection itself is contained in a relational schema, and it is identified by a schema-scoped [!INCLUDE[tsql](../../includes/tsql-md.md)] name. The following tuples are unique: xml_collection_id, and schema_id and name.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|xml_collection_id|**int**|ID of the XML schema collection. Unique within the database.|  
|schema_id|**int**|ID of the relational schema that contains this XML schema collection.|  
|principal_id|**int**|ID of the individual owner if different from the schema owner. By default, schema-contained objects are owned by the schema owner. However, an alternate owner may be specified by using the ALTER AUTHORIZATION statement to change ownership.<br /><br /> NULL = No alternate individual owner.|  
|name|**sysname**|Name of the XML schema collection.|  
|create_date|**datetime**|Date the XML schema collection was created.|  
|modify_date|**datetime**|Date the XML schema collection was last altered.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schemas &#40;XML Type System&#41; Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)   
 [Querying the SQL Server System Catalog FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.yml)  
  
  
