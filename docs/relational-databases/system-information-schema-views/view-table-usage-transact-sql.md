---
title: "VIEW_TABLE_USAGE (Transact-SQL)"
description: "VIEW_TABLE_USAGE (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "VIEW_TABLE_USAGE_TSQL"
  - "VIEW_TABLE_USAGE"
helpviewer_keywords:
  - "INFORMATION_SCHEMA.VIEW_TABLE_USAGE view"
  - "VIEW_TABLE_USAGE view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# VIEW_TABLE_USAGE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Returns one row for each table in the current database that is used in a view. This information schema view returns information about the objects to which the current user has permissions.  
  
 To retrieve information from these views, specify the fully qualified name of **INFORMATION_SCHEMA**.*view_name*.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**nvarchar(**128**)**|View qualifier.|  
|**VIEW_SCHEMA**|**nvarchar(**128**)**|Name of schema that contains the view.<br /><br /> **Important:** The only reliable way to find the schema of an object is to query the `sys.objects` catalog view.|  
|**VIEW_NAME**|**sysname**|View name.|  
|**TABLE_CATALOG**|**nvarchar(**128**)**|Table qualifier.|  
|**TABLE_SCHEMA**|**nvarchar(**128**)**|Name of schema that contains the base table.<br /><br /> **Important:** The only reliable way to find the schema of an object is to query the `sys.objects` catalog view.|  
|**TABLE_NAME**|**sysname**|Base table that the view is based on.|  
  
## See Also  
 [System Views &#40;Transact-SQL&#41;](../../t-sql/language-reference.md)   
 [Information Schema Views &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
