---
title: "sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)"
description: sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_os_buffer_pool_extension_configuration"
  - "sys.dm_os_buffer_pool_extension_configuration_TSQL"
  - "dm_os_buffer_pool_extension_configuration_TSQL"
  - "sys.dm_os_buffer_pool_extension_configuration"
helpviewer_keywords:
  - "sys.dm_os_buffer_pool_extension_configuration dynamic management view"
dev_langs:
  - "TSQL"
---
# sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  Returns configuration information about the buffer pool extension in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Returns one row for each buffer pool extension file.  
  

  
| Column name | Data type | Description |
| :---------- | :-------- | :---------- |
|path|**nvarchar**(256)|Path and file name of the buffer pool extension cache. Nullable.|  
|file_id|**int**|ID of the buffer pool extension file. Is not nullable.|  
|state|**int**|The state of the buffer pool extension feature. Is not nullable.<br /><br /> 0 - Buffer pool extension disabled<br /><br /> 1 - Buffer pool extension disabling<br /><br /> 2 - Reserved for the future use<br /><br /> 3 - Buffer pool extension enabling<br /><br /> 4 - Reserved for the future use<br /><br /> 5 - Buffer pool extension enabled|  
|state_description|**nvarchar**(60)|Describes the state of the buffer pool extension feature. Is nullable.<br /><br /> 0 = BUFFER POOL EXTENSION DISABLED<br /><br /> 5 = BUFFER POOL EXTENSION ENABLED|
|current_size_in_kb|**bigint**|Current size of the buffer pool extension file. Is not nullable.|

## Permissions  
 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## Examples  
  
### A. Returning configuration buffer pool extension information  
 The following example returns all columns from the sys.dm_os_buffer_pool_extension_configruation DMV.  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### B. Returning the number of cached pages in the buffer pool extension file  
 The following example returns the number of cached pages in each buffer pool extension file.  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## See also  
 [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
