---
title: "sys.event_notifications (Transact-SQL)"
description: sys.event_notifications (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "event_notifications_TSQL"
  - "event_notifications"
  - "sys.event_notifications_TSQL"
  - "sys.event_notifications"
helpviewer_keywords:
  - "sys.event_notifications catalog view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.event_notifications (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns a row for each object that is an event notification, with **sys.objects.type** = EN.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Event notification name.|  
|**object_id**|**int**|Object identification number. Is unique within a database.|  
|**parent_class**|**tinyint**|Class of parent.<br /><br /> 0 = Database<br /><br /> 1 = Object or Column|  
|**parent_class_desc**|**nvarchar(60)**|DATABASE<br /><br /> OBJECT_OR_COLUMN|  
|**parent_id**|**int**|Non-zero ID of the parent object.<br /><br /> 0 = The parent class is the database.|  
|**create_date**|**datetime**|Date created.|  
|**modify_date**|**datetime**|Always equals **create_date**.|  
|**service_name**|**nvarchar(256)**|Name of the target service to which the notification is sent.|  
|**broker_instance**|**nvarchar(128)**|Broker instance to which the notification is sent.|  
|**principal_id**|**int**|ID of the database principal that owns this event notification.|  
|**creator_sid**|**varbinary(85)**|SID of the login who created the event notification.<br /><br /> Is NULL if the FAN_IN option is not specified.|  
  
## Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## See Also  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
