---
title: "ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)"
description: ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "04/20/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ALTER_CRYPTOGRAPHIC_PROVIDER_TSQL"
  - "ALTER CRYPTOGRAPHIC PROVIDER"
  - "ALTER_CRYPTOGRAPHIC_TSQL"
  - "ALTER CRYPTOGRAPHIC"
helpviewer_keywords:
  - "ALTER CRYPTOGRAPHIC PROVIDER"
dev_langs:
  - "TSQL"
---
# ALTER CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Alters a cryptographic provider within [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] from an Extensible Key Management (EKM) provider.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
ALTER CRYPTOGRAPHIC PROVIDER provider_name   
    [ FROM FILE = path_of_DLL ]  
    ENABLE | DISABLE  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *provider_name*  
 Name of the Extensible Key Management provider.  
  
 *Path_of_DLL*  
 Path of the .dll file that implements the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Extensible Key Management interface.  
  
 ENABLE | DISABLE  
 Enables or disables a provider.  
  
## Remarks  
 If the provider changes the .dll file that is used to implement Extensible Key Management in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], you must use the ALTER CRYPTOGRAPHIC PROVIDER statement.  
  
 When the .dll file path is updated by using the ALTER CRYPTOGRAPHIC PROVIDER statement, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] performs the following actions:  
-   Disables the provider.  
-   Verifies the DLL signature and ensures that the .dll file has the same GUID as the one recorded in the catalog.  
-   Updates the DLL version in the catalog.  
  

When an EKM provider is set to DISABLE, any attempts on new connections to use the provider with encryption statements will fail.  
  
To disable a provider, all sessions that use the provider must be terminated.  
  
When an EKM provider dll does not implement all of the necessary methods, ALTER CRYPTOGRAPHIC PROVIDER can return error 33085:  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
When the header file used to create the EKM provider dll is out of date, ALTER CRYPTOGRAPHIC PROVIDER can return error 33032:  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## Permissions  
 Requires CONTROL permission on the cryptographic provider.  
  
## Examples  
 The following example alters a cryptographic provider, called `SecurityProvider` in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], to a newer version of a .dll file. This new version is named `c:\SecurityProvider\SecurityProvider_v2.dll` and is installed on the server. The provider's certificate must be installed on the server.  
  
1. Disable the provider to perform the upgrade. This will terminate all open cryptographic sessions.  
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
DISABLE;  
GO  
```  

2. Upgrade the provider .dll file. The GUID must the same as the previous version, but the version can be different.  
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider  
FROM FILE = 'c:\SecurityProvider\SecurityProvider_v2.dll';  
GO  
```  

3. Enable the upgraded provider.   
```sql  
ALTER CRYPTOGRAPHIC PROVIDER SecurityProvider   
ENABLE;  
GO  
```  
  
## See Also  
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Extensible Key Management Using Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  
