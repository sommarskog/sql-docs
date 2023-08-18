---
title: "sys.partition_range_values (Transact-SQL)"
description: sys.partition_range_values (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.partition_range_values"
  - "partition_range_values_TSQL"
  - "partition_range_values"
  - "sys.partition_range_values_TSQL"
helpviewer_keywords:
  - "sys.partition_range_values catalog view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# sys.partition_range_values (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Contains a row for each range boundary value of a partition function of type R.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|ID of the partition function for this range boundary value.|  
|**boundary_id**|**int**|ID (1-based ordinal) of the boundary value tuple, with left-most boundary starting at an ID of 1.|  
|**parameter_id**|**int**|ID of the parameter of the function to which this value corresponds. The values in this column correspond with those in the **parameter_id** column of the **sys.partition_parameters** catalog view for any particular **function_id**.|  
|**value**|**sql_variant**|The actual boundary value.|  
  
## Permissions  
 Requires membership in the **public** role. For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Partition Function Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
