---
title: "sys.dm_database_encryption_keys (Transact-SQL)"
description: sys.dm_database_encryption_keys (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/24/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_database_encryption_keys"
  - "sys.dm_database_encryption_keys_TSQL"
  - "dm_database_encryption_keys"
  - "dm_database_encryption_keys_TSQL"
helpviewer_keywords:
  - "sys.dm_database_encryption_keys dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns information about the encryption state of a database and its associated database encryption keys. For more information about database encryption, see [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|Column Name|Data Type|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID of the database.|  
|encryption_state|**int**|Indicates whether the database is encrypted or not encrypted.<br /><br /> 0 = No database encryption key present, no encryption<br /><br /> 1 = Unencrypted<br /><br /> 2 = Encryption in progress<br /><br /> 3 = Encrypted<br /><br /> 4 = Key change in progress<br /><br /> 5 = Decryption in progress<br /><br /> 6 = Protection change in progress (The certificate or asymmetric key that is encrypting the database encryption key is being changed.)|  
|create_date|**datetime**|Displays the date (in UTC) the encryption key was created.|  
|regenerate_date|**datetime**|Displays the date (in UTC) the encryption key was regenerated.|  
|modify_date|**datetime**|Displays the date (in UTC) the encryption key was modified.|  
|set_date|**datetime**|Displays the date (in UTC) the encryption key was applied to the database.|  
|opened_date|**datetime**|Shows when (in UTC) the database key was last opened.|  
|key_algorithm|**nvarchar(32)**|Displays the algorithm that is used for the key.|  
|key_length|**int**|Displays the length of the key.|  
|encryptor_thumbprint|**varbinary(20)**|Shows the thumbprint of the encryptor.|  
|encryptor_type|**nvarchar(32)**|**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] through [current version](/troubleshoot/sql/general/determine-version-edition-update-level)).<br /><br /> Describes the encryptor.|  
|percent_complete|**real**|Percent complete of the database encryption state change. This will be 0 if there is no state change.|
|encryption_state_desc|**nvarchar(32)**|**Applies to**: [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)] and later.<br><br> String that indicates whether the database is encrypted or not encrypted.<br><br>NONE<br><br>UNENCRYPTED<br><br>ENCRYPTED<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**Applies to**: [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)] and later.<br><br>Indicates the current state of the encryption scan. <br><br>0 = No scan has been initiated, TDE is not enabled<br><br>1 = Scan is in progress.<br><br>2 = Scan is in progress but has been suspended, user can resume.<br><br>3 = Scan was aborted for some reason, manual intervention is required. Contact Microsoft Support for more assistance.<br><br>4 = Scan has been successfully completed, TDE is enabled and encryption is complete.|
|encryption_scan_state_desc|**nvarchar(32)**|**Applies to**: [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)] and later.<br><br>String that indicates the current state of the encryption scan.<br><br> NONE<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>COMPLETE|
|encryption_scan_modify_date|**datetime**|**Applies to**: [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)] and later.<br><br> Displays the date (in UTC) the encryption scan state was last modified.|
  
## Permissions

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   

### Permissions for SQL Server 2022 and later

Requires VIEW SERVER SECURITY STATE permission on the server.

## See also  

 [Security-Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server Encryption](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server and Database Encryption Keys &#40;Database Engine&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET Options &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
