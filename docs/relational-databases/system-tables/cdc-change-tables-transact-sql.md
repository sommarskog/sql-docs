---
title: "cdc.change_tables (Transact-SQL)"
description: cdc.change_tables (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "02/22/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "cdc.change_tables"
  - "cdc.change_tables_TSQL"
helpviewer_keywords:
  - "cdc.change_tables"
dev_langs:
  - "TSQL"
---
# cdc.change_tables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns one row for each change table in the database. A change table is created when change data capture is enabled on a source table. We recommend that you don't query the system tables directly. Instead, execute the [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) stored procedure.  

|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID of the change table. Is unique within a database.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> For [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], this column always returns 0.|  
|**source_object_id**|**int**|ID of the source table enabled for change data capture.|  
|**capture_instance**|**sysname**|Name of the capture instance used to name instance-specific tracking objects. By default, the name is derived from the source schema name plus the source table name in the format *schemaname_sourcename*.|  
|**start_lsn**|**binary(10)**|Log sequence number (LSN) representing the low endpoint when querying for change data in the change table.<br /><br /> NULL = the low endpoint hasn't been established.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> For [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)], this column always returns NULL.|  
|**supports_net_changes**|**bit**|Support for querying for net changes is enabled for the change table.|  
|**has_drop_pending**|**bit**|Capture process has received notification that the source table has been dropped.|  
|**role_name**|**sysname**|Name of the database role used to gate access to change data.<br /><br /> NULL = a role isn't used.|  
|**index_name**|**sysname**|Name of the index used to uniquely identify rows in the source table. **index_name** is either the name of the primary key index of the source table, or the name of a unique index specified when change data capture was enabled on the source table.<br /><br /> NULL = source table didn't have a primary key when change data capture was enabled and a unique index wasn't specified when change data capture was enabled.<br /><br /> Note: If change data capture is enabled on a table where a primary key exists, the change data capture feature uses the index regardless of whether net changes are enabled or not. After change data capture is enabled, no modification is allowed on the primary key. If there's no primary key on the table, you can still enable change data capture but only with net changes set to false. After change data capture is enabled, you can then create a primary key. You can also modify the primary key because change data capture doesn't use the primary key.|  
|**filegroup_name**|**sysname**|Name of the filegroup in which the change table resides.<br /><br /> NULL = change table is in the default filegroup of the database.|  
|**create_date**|**datetime**|Date that the source table was enabled.|  
|**partition_switch**|**bit**|Indicates whether the **SWITCH PARTITION** command of **ALTER TABLE** can be executed against a table that is enabled for change data capture. 0 indicates that partition switching is blocked. Non-partitioned tables always return 1.|  
  
## See Also  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
