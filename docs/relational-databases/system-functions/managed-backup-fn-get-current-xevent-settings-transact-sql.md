---
title: "managed_backup.fn_get_current_xevent_settings (Transact-SQL)"
description: "managed_backup.fn_get_current_xevent_settings (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "fn_get_current_xevent_settings"
  - "smart_admin.fn_get_current_xevent_settings_TSQL"
  - "fn_get_current_xevent_settings_TSQL"
  - "smart_admin.fn_get_current_xevent_settings"
helpviewer_keywords:
  - "smart_admin.fn_get_current_xevent_settings"
  - "fn_get_current_xevent_settings"
dev_langs:
  - "TSQL"
---
# managed_backup.fn_get_current_xevent_settings (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Returns 1 row for each Extended Event type supported by Smart Admn.  
  
 Use this function to return or review the current Extended Event settings to identify the type of events that are configurable and the current configurations.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="Arguments"></a> Arguments  
 This function does not have any arguments.  
  
## Table Returned  
 Admin, analytic, and operational channels of the Extended Events are necessary are enabled by default and not configurable.  
  
|Column Name|Data Type|Description|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR(128)|Extended Event type|  
|is_configurable|NVARCHAR(128)|This is set to **True** if the event is configurable, else it set to **False**.|  
|is_enabled|NVARCHAR(128)|This is set to True if the event is enabled, set to False if it is not enabled. Use the smart_admin.sp_set_parameter to enable debug events.|  
  
## Security  
  
### Permissions  
 Requires **SELECT** permissions on the function.  
  
## Examples  
 The following example returns all the Extended Events with their current status.  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
