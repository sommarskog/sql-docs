---
title: "sysarticlecolumns (System View) (Transact-SQL)"
description: "sysarticlecolumns (System View) (Transact-SQL)"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sysarticlecolumns"
  - "sysarticlecolumns_TSQL"
helpviewer_keywords:
  - "sysarticlecolumns view"
dev_langs:
  - "TSQL"
---

# sysarticlecolumns (System View) (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

The **sysarticlecolumns** view exposes additional information about columns in published articles. This view is stored in the distribution database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifies an article.|  
|**colid**|**int**|Identifies a column in an article.|  
|**is_udt**|**int**|Indicates whether the column is a user-defined data type (UDT) column. A value of **1** indicates a UDT column.|  
|**is_xml**|**int**|Is if the column is an **xml** column. A value of **1** indicates an **xml** column.|  
|**is_max**|**int**|Is if the column is a Large Value data type column (**varchar(max)**, **nvarchar(max)** or **varbinary(max)**). A value of **1** indicates a Large Value column.|  
  
## See Also  
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
