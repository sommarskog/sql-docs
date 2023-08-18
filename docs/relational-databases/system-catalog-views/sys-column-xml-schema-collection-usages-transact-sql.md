---
title: "sys.column_xml_schema_collection_usages (Transact-SQL)"
description: sys.column_xml_schema_collection_usages (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "column_xml_schema_collection_usages_TSQL"
  - "sys.column_xml_schema_collection_usages"
  - "column_xml_schema_collection_usages"
  - "sys.column_xml_schema_collection_usages_TSQL"
helpviewer_keywords:
  - "sys.column_xml_schema_collection_usages catalog view"
dev_langs:
  - "TSQL"
---
# sys.column_xml_schema_collection_usages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns a row for each column that is validated by an XML schema.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|The ID of the object to which this column belongs.|  
|**column_id**|**int**|The ID of the column. Is unique within the object.|  
|**xml_collection_id**|**int**|The ID of the collection that contains the validating XML schema namespace of the column.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [XML Schemas &#40;XML Type System&#41; Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
