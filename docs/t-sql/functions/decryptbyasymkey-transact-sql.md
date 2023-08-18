---
title: "DECRYPTBYASYMKEY (Transact-SQL)"
description: "DECRYPTBYASYMKEY (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "DECRYPTBYASYMKEY"
  - "DECRYPTBYASYMKEY_TSQL"
helpviewer_keywords:
  - "asymmetric keys [SQL Server], DECRYPTBYASYMKEY function"
  - "DECRYPTBYASYMKEY function"
  - "decryption [SQL Server], asymmetric keys"
dev_langs:
  - "TSQL"
---
# DECRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

This function uses an asymmetric key to decrypt encrypted data.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *Asym_Key_ID*  
The ID of an asymmetric key in the database. *Asym_Key_ID* has an **int** data type.  
  
 *ciphertext*  
The string of data encrypted with the asymmetric key.  
  
 @ciphertext  
A variable of type **varbinary**, containing data encrypted with the asymmetric key.  
  
 *Asym_Key_Password*  
The password used to encrypt the asymmetric key in the database.  
  
## Return Types  
**varbinary**, with a maximum size of 8,000 bytes.  
  
## Remarks  
Compared to symmetric encryption / decryption, asymmetric key encryption / decryption has a high cost. When working with large datasets - for example, user data stored in tables - we suggest that developers avoid asymmetric key encryption / decryption.  
  
## Permissions  
`DECRYPTBYASYMKEY` requires CONTROL permission on the asymmetric key.  
  
## Examples  
This example decrypts ciphertext originally encrypted with asymmetric key `JanainaAsymKey02`. `AdventureWorks2022.ProtectedData04` stored this asymmetric key. The example decrypted the returned data with asymmetric key `JanainaAsymKey02`. The example used password `pGFD4bb925DGvbd2439587y` to decrypt this asymmetric key. The example converted the returned plaintext to type **nvarchar**.  
  
```sql
SELECT CONVERT(NVARCHAR(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2022].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## See Also  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
