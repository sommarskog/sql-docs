---
title: "sys.sysmembers (Transact-SQL)"
description: "sys.sysmembers (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.sysmembers_TSQL"
  - "sysmembers"
  - "sys.sysmembers"
  - "sysmembers_TSQL"
helpviewer_keywords:
  - "sysmembers system table"
  - "sys.sysmembers compatibility view"
dev_langs:
  - "TSQL"
---
# sys.sysmembers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contains a row for each member of a database role.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**memberuid**|**smallint**|User ID for the role member. Overflows or returns NULL if the number of users and roles exceeds 32,767.|  
|**groupuid**|**smallint**|User ID for the role. Overflows or returns NULL if the number of users and roles exceeds 32,767.|  
  
## See Also  
 [Mapping System Tables to System Views &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Compatibility Views &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
