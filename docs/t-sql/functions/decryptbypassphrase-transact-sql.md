---
title: "DECRYPTBYPASSPHRASE (Transact-SQL)"
description: "DECRYPTBYPASSPHRASE (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "DECRYPTBYPASSPHRASE"
  - "DECRYPTBYPASSPHRASE_TSQL"
helpviewer_keywords:
  - "decryption [SQL Server], symmetric keys"
  - "symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function"
  - "DECRYPTBYPASSPHRASE function"
dev_langs:
  - "TSQL"
---
# DECRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

This function decrypts data originally encrypted with a passphrase.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *passphrase*  
The passphrase used to generate the decryption key.  
  
 @passphrase  
A variable of type **char**, **nchar**, **nvarchar**, or **varchar** containing the passphrase used to generate the decryption key.  
  
'*ciphertext*'  
The string of data encrypted with the key. *ciphertext* has a **varbinary** data type.  
 
@ciphertext  
A variable of type **varbinary** containing data encrypted with the key. The *\@ciphertext* variable has a maximum size of 8,000 bytes.  
  
*add_authenticator*  
Indicates whether the original encryption process included, and encrypted, an authenticator together with the plaintext. *add_authenticator* has a value of 1 if the encryption process used an authenticator. *add_authenticator* has an **int** data type.  
  
@add_authenticator  
A variable indicating whether the original encryption process included, and encrypted, an authenticator together with the plaintext. Is *\@add_authenticator* has a value of 1 if the encryption process used an authenticator. *\@add_authenticator* has an **int** data type.  

*authenticator*  
The data used as the basis for the generation of the authenticator. *authenticator* has a **sysname** data type.  
  
@authenticator  
A variable containing data used as the basis for the generation of the authenticators. *\@authenticator* has a **sysname** data type.  
  
## Return Types  
**varbinary**, with a maximum size of 8,000 bytes.  
  
## Remarks  
`DECRYPTBYPASSPHRASE` requires no permissions for its execution. `DECRYPTBYPASSPHRASE` returns NULL if it receives the wrong passphrase or the wrong authenticator information.  
  
`DECRYPTBYPASSPHRASE` uses the passphrase to generate a decryption key. This decryption key will not persist.  
  
If an authenticator was included at the time of the ciphertext encryption, `DECRYPTBYPASSPHRASE` must receive that same authenticator for the decryption process. If the authenticator value provided for the decryption process does not match the authenticator value originally used to encrypted the data, the `DECRYPTBYPASSPHRASE` operation will fail.  
  
## Examples  
This example decrypts the record updated in [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md).  
  
```sql  
USE AdventureWorks2022;  
-- Get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser NVARCHAR(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(varchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## See Also  
 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  
