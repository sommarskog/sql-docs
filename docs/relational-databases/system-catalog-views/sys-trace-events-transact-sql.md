---
title: "sys.trace_events (Transact-SQL)"
description: sys.trace_events (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "08/09/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "trace_events_TSQL"
  - "trace_events"
  - "sys.trace_events"
  - "sys.trace_events_TSQL"
helpviewer_keywords:
  - "sys.trace_events catalog view"
dev_langs:
  - "TSQL"
---
# sys.trace_events (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  The **sys.trace_events** catalog view contains a list of all SQL trace events. These trace events do not change for a given version of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use Extended Event catalog views instead.  
  
 For more information about these trace events, see [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**trace_event_id**|**smallint**|Unique ID of the event. This column is also in the **sys.trace_event_bindings** and **sys.trace_subclass_values** catalog views.|  
|**category_id**|**smallint**|Category ID of the event. This column is also in the **sys.trace_categories** catalog view.|  
|**name**|**nvarchar(128)**|Unique name of this event. This parameter is not localized.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See also  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.traces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys.trace_categories &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-columns-transact-sql.md)   
 [sys.trace_event_bindings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
