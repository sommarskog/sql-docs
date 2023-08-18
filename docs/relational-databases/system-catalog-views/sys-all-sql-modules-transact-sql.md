---
title: "sys.all_sql_modules (Transact-SQL)"
description: sys.all_sql_modules (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/17/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "all_sql_modules_TSQL"
  - "sys.all_sql_modules"
  - "all_sql_modules"
  - "sys.all_sql_modules_TSQL"
helpviewer_keywords:
  - "sys.all_sql_modules catalog view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# sys.all_sql_modules (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Returns the union of **sys.sql_modules** and **sys.system_sql_modules**.  
  
 The view returns a row for each natively compiled, scalar user-defined function. For more information, see [Scalar User-Defined Functions for In-Memory OLTP](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID of the object of the containing object. Is unique within a database.|  
|**definition**|**nvarchar(max)**|SQL text that defines this module.<br /><br /> NULL = Encrypted|  
|**uses_ansi_nulls**|**bit**|Module was created with SET ANSI_NULLS ON.|  
|**uses_quoted_identifier**|**bit**|Module was created with SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|Module was created with the SCHEMABINDING option.|  
|**uses_database_collation**|**bit**|1 = Schema-bound module definition depends on the default-collation of the database for correct evaluation; otherwise, 0. Such a dependency prevents changing the default collation of the database.|  
|**is_recompiled**|**bit**|Procedure was created using the WITH RECOMPILE option.|  
|**null_on_null_input**|**bit**|Module was declared to produce a NULL output on any NULL input.|  
|**execute_as_principal_id**|**int**|ID of the EXECUTE AS database principal.<br /><br /> NULL by default or if EXECUTE AS CALLER.<br /><br /> ID of the specified principal if EXECUTE AS SELF or EXECUTE AS \<principal>.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|bit|**Applies to**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] and later.<br /><br /> 0 = not natively compiled<br /><br /> 1 = is natively compiled<br /><br /> The default value is 0.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.system_sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [In-Memory OLTP &#40;In-Memory Optimization&#41;](../in-memory-oltp/overview-and-usage-scenarios.md)  
  
