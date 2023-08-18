---
title: "OPEN SYMMETRIC KEY (Transact-SQL)"
description: OPEN SYMMETRIC KEY (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "OPEN SYMMETRIC KEY"
  - "OPEN_SYMMETRIC_KEY_TSQL"
helpviewer_keywords:
  - "symmetric keys [SQL Server], opening"
  - "OPEN SYMMETRIC KEY statement"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest"
---
# OPEN SYMMETRIC KEY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Decrypts a symmetric key and makes it available for use.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
## Syntax  
  
```syntaxsql
OPEN SYMMETRIC KEY Key_name DECRYPTION BY <decryption_mechanism>  
  
<decryption_mechanism> ::=  
    CERTIFICATE certificate_name [ WITH PASSWORD = 'password' ]  
    |  
    ASYMMETRIC KEY asym_key_name [ WITH PASSWORD = 'password' ]  
    |  
    SYMMETRIC KEY decrypting_Key_name  
    |  
    PASSWORD = 'decryption_password'  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *Key_name*  
 Is the name of the symmetric key to be opened.  
  
 CERTIFICATE *certificate_name*  
 Is the name of a certificate whose private key will be used to decrypt the symmetric key.  
  
 ASYMMETRIC KEY *asym_key_name*  
 Is the name of an asymmetric key whose private key will be used to decrypt the symmetric key.  
  
 WITH PASSWORD ='*password*'  
 Is the password that was used to encrypt the private key of the certificate or asymmetric key.  
  
 SYMMETRIC KEY *decrypting_key_name*  
 Is the name of a symmetric key that will be used to decrypt the symmetric key that is being opened.  
  
 PASSWORD ='*password*'  
 Is the password that was used to protect the symmetric key.  
  
## Remarks  
 Open symmetric keys are bound to the session not to the security context. An open key will continue to be available until it is either explicitly closed or the session is terminated. If you open a symmetric key and then switch context, the key will remain open and be available in the impersonated context. Multiple keys can be open at once. Information about open symmetric keys is visible in the [sys.openkeys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md) catalog view.  
  
 If the symmetric key was encrypted with another key, that key must be opened first.  
  
 If the symmetric key is already open, the query is a **NO_OP**.  
  
 If the password, certificate, or key supplied to decrypt the symmetric key is incorrect, the query will fail.  
  
 Symmetric keys created from encryption providers cannot be opened. Encryption and decryption operations using this kind of symmetric key succeed without the **OPEN** statement because the Encryption Provider is opening and closing the key.  
  
## Permissions  
 The caller must have some permission on the key and must not have been denied VIEW DEFINITION permission on the key. Additional requirements vary, depending on the decryption mechanism:  
  
-   DECRYPTION BY CERTIFICATE: CONTROL permission on the certificate and knowledge of the password that encrypts its private key.  
  
-   DECRYPTION BY ASYMMETRIC KEY: CONTROL permission on the asymmetric key and knowledge of the password that encrypts its private key.  
  
-   DECRYPTION BY PASSWORD: knowledge of one of the passwords that is used to encrypt the symmetric key.  
  
## Examples  
  
### A. Opening a symmetric key by using a certificate  
 The following example opens the symmetric key `SymKeyMarketing3` and decrypts it by using the private key of certificate `MarketingCert9`.  
  
```sql  
USE AdventureWorks2022;  
OPEN SYMMETRIC KEY SymKeyMarketing3   
    DECRYPTION BY CERTIFICATE MarketingCert9;  
GO  
```  
  
### B. Opening a symmetric key by using another symmetric key  
 The following example opens the symmetric key `MarketingKey11` and decrypts it by using symmetric key `HarnpadoungsatayaSE3`.  
  
```sql  
USE AdventureWorks2022;  
-- First open the symmetric key that you want for decryption.  
OPEN SYMMETRIC KEY HarnpadoungsatayaSE3   
    DECRYPTION BY CERTIFICATE sariyaCert01;  
-- Use the key that is already open to decrypt MarketingKey11.  
OPEN SYMMETRIC KEY MarketingKey11   
    DECRYPTION BY SYMMETRIC KEY HarnpadoungsatayaSE3;  
GO   
```  
  
## See Also  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
