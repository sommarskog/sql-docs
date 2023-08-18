---
title: "sys.server_events (Transact-SQL)"
description: sys.server_events (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "server_events_TSQL"
  - "sys.server_events_TSQL"
  - "server_events"
  - "sys.server_events"
helpviewer_keywords:
  - "sys.server_events catalog view"
dev_langs:
  - "TSQL"
---
# sys.server_events (Transact-SQL)
[!INCLUDE [sqlserver-asdbmi](../../includes/applies-to-version/sql-asdbmi.md)]

  Contains one row for each event for which a server-level event-notification or server-level DDL trigger fires. The columns **object_id** and **type** uniquely identify the server event.  

  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID of the server-level event notification or server-level DDL trigger to fire.|  
|**type**|**int**|Type of the event that causes the event notification or DDL trigger to fire.|  
|**type_desc**|**nvarchar(60)**|Description of the event that causes the DDL trigger or event notification to fire.|  
|**event_group_type**|**int**|Event group on which the trigger or event notification is created, or null if not created on an event group.|  
|**event_group_type_desc**|**nvarchar(60)**|Description of the event group on which the trigger or event notification is created, or null if not created on an event group|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
