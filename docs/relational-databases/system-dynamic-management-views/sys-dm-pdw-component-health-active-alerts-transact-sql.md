---
title: "sys.dm_pdw_component_health_active_alerts (Transact-SQL"
description: sys.dm_pdw_component_health_active_alerts (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/07/2017"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: conceptual
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016"
---
# sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Stores active alerts on [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] components.  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Unique identifier of a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] node.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, and alert_instance_id form the key for this view.|NOT NULL|  
|component_id|**int**|The ID of the component. See [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, and alert_instance_id form the key for this view.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|pdw_node_id, component_id, component_instance_id, alert_id, and alert_instance_id form the key for this view.|NOT NULL|  
|alert_id|**int**|The ID for the alert type. See [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, and alert_instance_id form the key for this view.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifies an instance of a given alert.<br /><br /> pdw_node_id, component_id, component_instance_id, alert_id, and alert_instance_id form the key for this view.|NOT NULL|  
|current_value|**nvarchar(255)**|Used when the alert is of type StatusChange. This is the current component status. Value is NULL for alerts of type Threshold. See [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) for a list of alert types.|NULL|  
|previous_value|**nvarchar(255)**|Used when the alert is of type StatusChange. This is the previous component status. Value is NULL for alerts of type Threshold. See [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) for a list of alert types.|NULL|  
|create_time|**datetime**|Time and date when the alert was generated.|NOT NULL|  
  
 For information about the maximum rows retained by this view, see "Minimum and Maximum Values" in the [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
