---
title: "sys.fn_MSxe_read_event_stream (Transact-SQL)"
description: "sys.fn_MSxe_read_event_stream (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "fn_MSxe_read_event_stream_TSQL"
  - "sys.fn_MSxe_read_event_stream_TSQL"
  - "sys.fn_MSxe_read_event_stream"
  - "fn_MSxe_read_event_stream"
helpviewer_keywords:
  - "sys.fn_MSxe_read_event_stream"
  - "fn_MSxe_read_event_stream"
dev_langs:
  - "TSQL"
---
# sys.fn_MSxe_read_event_stream (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Extended Events provides a table valued function (TVF) for internal use by the Extended Events user interface (UI). The table does not provide customer usable data.  
  
 To view event data, use one of the following:  
  
-   Extended Events New Session UI.  
  
-   fn_xe_file_target_read_file TVF. For more information, see [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md).  
  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sys.fn_MSxe_read_event_stream ( session_name)  
```  
  
## Arguments  
 *Session_name*  
 The name of a session that is running on the server.  
  
## Table Returned  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|type|**Integer (4)**|The event type. Is not nullable.|  
|data|**Image (16)**|The event image data. Is nullable.|  
  
## See Also  
 [Extended Events Dynamic Management Views](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Extended Events Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Extended Events](../../relational-databases/extended-events/extended-events.md)  
  
  
