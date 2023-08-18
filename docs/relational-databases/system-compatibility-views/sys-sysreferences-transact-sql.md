---
title: "sys.sysreferences (Transact-SQL)"
description: "sys.sysreferences (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.sysreferences"
  - "sys.sysreferences_TSQL"
  - "sysreferences"
  - "sysreferences_TSQL"
helpviewer_keywords:
  - "sys.sysreferences compatibility view"
  - "sysreferences system table"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# sys.sysreferences (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Contains mappings of the FOREIGN KEY constraint definitions to the referenced columns within the database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|ID of the FOREIGN KEY constraint.|  
|**fkeyid**|**int**|ID of the referencing table.|  
|**rkeyid**|**int**|ID of the referenced table.|  
|**rkeyindid**|**smallint**|Index ID of the unique index on the referenced table covering the referenced key-columns.|  
|**keycnt**|**smallint**|Number of columns in the key.|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|Reserved.|  
|**rkeydbid**|**smallint**|Reserved.|  
|**fkey1**|**smallint**|Column ID of the referencing column.|  
|**fkey2**|**smallint**|Column ID of the referencing column.|  
|**fkey3**|**smallint**|Column ID of the referencing column.|  
|**fkey4**|**smallint**|Column ID of the referencing column.|  
|**fkey5**|**smallint**|Column ID of the referencing column.|  
|**fkey6**|**smallint**|Column ID of the referencing column.|  
|**fkey7**|**smallint**|Column ID of the referencing column.|  
|**fkey8**|**smallint**|Column ID of the referencing column.|  
|**fkey9**|**smallint**|Column ID of the referencing column.|  
|**fkey10**|**smallint**|Column ID of the referencing column.|  
|**fkey11**|**smallint**|Column ID of the referencing column.|  
|**fkey12**|**smallint**|Column ID of the referencing column.|  
|**fkey13**|**smallint**|Column ID of the referencing column.|  
|**fkey14**|**smallint**|Column ID of the referencing column.|  
|**fkey15**|**smallint**|Column ID of the referencing column.|  
|**fkey16**|**smallint**|Column ID of the referencing column.|  
|**rkey1**|**smallint**|Column ID of the referenced column.|  
|**rkey2**|**smallint**|Column ID of the referenced column.|  
|**rkey3**|**smallint**|Column ID of the referenced column.|  
|**rkey4**|**smallint**|Column ID of the referenced column.|  
|**rkey5**|**smallint**|Column ID of the referenced column.|  
|**rkey6**|**smallint**|Column ID of the referenced column.|  
|**rkey7**|**smallint**|Column ID of the referenced column.|  
|**rkey8**|**smallint**|Column ID of the referenced column.|  
|**rkey9**|**smallint**|Column ID of the referenced column.|  
|**rkey10**|**smallint**|Column ID of the referenced column.|  
|**rkey11**|**smallint**|Column ID of the referenced column.|  
|**rkey12**|**smallint**|Column ID of the referenced column.|  
|**rkey13**|**smallint**|Column ID of the referenced column.|  
|**rkey14**|**smallint**|Column ID of the referenced column.|  
|**rkey15**|**smallint**|Column ID of the referenced column.|  
|**rkey16**|**smallint**|Column ID of the referenced column.|  
  
## See Also  
 [Mapping System Tables to System Views &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Compatibility Views &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
