---
title: "sys.database_scoped_credentials (Transact-SQL)"
description: sys.database_scoped_credentials (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/27/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: conceptual
f1_keywords:
  - "sys.database_scoped_credentials"
  - "sys.database_scoped_credentials_TSQL"
  - "database_scoped_credentials"
  - "database_scoped_credentials_TSQL"
helpviewer_keywords:
  - "sys.database_scoped_credentials catalog view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.database_scoped_credentials (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Returns one row for each database scoped credential in the database.  
  
::: moniker range="=sql-server-2016"
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Name of the database scoped credential. Is unique in the database.|  
|credential_id|**int**|ID of the database scoped credential. Is unique in the database.|  
|credential_identity|**nvarchar(4000)**|Name of the identity to use. This will generally be a Windows user. It does not have to be unique.|  
|create_date|**datetime**|Time at which the database scoped credential was created.|  
|modify_date|**datetime**|Time at which the database scoped credential was last modified.|  
|target_type|**nvarchar(100)**|Type of database scoped credential. Returns `NULL` for database scoped credentials.|  
|target_id|**int**|ID of the object that the database scoped credential is mapped to. Returns 0 for database scoped credentials|  
::: moniker-end
  
::: moniker range=">=sql-server-2017||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current"
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Name of the database scoped credential. Is unique in the database.|  
|credential_id|**int**|ID of the database scoped credential. Is unique in the database.|  
|principal_id|**int**|ID of the database principal who owns the key.|  
|credential_identity|**nvarchar(4000)**|Name of the identity to use. This will generally be a Windows user. It does not have to be unique.|  
|create_date|**datetime**|Time at which the database scoped credential was created.|  
|modify_date|**datetime**|Time at which the database scoped credential was last modified.|  
|target_type|**nvarchar(100)**|Type of database scoped credential. Returns `NULL` for database scoped credentials.|  
|target_id|**int**|ID of the object that the database scoped credential is mapped to. Returns 0 for database scoped credentials|  
::: moniker-end

## Permissions  
 Requires `CONTROL` permission on the database.  
  
## See Also  
 [Credentials &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
