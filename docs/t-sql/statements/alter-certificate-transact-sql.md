---
title: "ALTER CERTIFICATE (Transact-SQL)"
description: ALTER CERTIFICATE (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "04/22/2019"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ALTER_CERTIFICATE_TSQL"
  - "ALTER CERTIFICATE"
helpviewer_keywords:
  - "ENCRYPTION BY PASSWORD option"
  - "encryption [SQL Server], certificates"
  - "modifying certificates"
  - "private keys [SQL Server]"
  - "ALTER CERTIFICATE statement"
  - "certificates [SQL Server], modifying"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# ALTER CERTIFICATE (Transact-SQL)

[!INCLUDE [sql-asdb-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-pdw.md)]

  Changes the password used to encrypt the private key of a certificate, removes the private key, or imports the private key if none is present. Changes the availability of a certificate to [!INCLUDE[ssSB](../../includes/sssb-md.md)].  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER CERTIFICATE certificate_name   
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY ( <private_key_spec> )  
    | WITH ACTIVE FOR BEGIN_DIALOG = { ON | OFF }  
  
<private_key_spec> ::=   
      {   
        { FILE = 'path_to_private_key' | BINARY = private_key_bits }  
         [ , DECRYPTION BY PASSWORD = 'current_password' ]  
         [ , ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
    |  
      {  
         [ DECRYPTION BY PASSWORD = 'current_password' ]  
         [ [ , ] ENCRYPTION BY PASSWORD = 'new_password' ]  
      }  
``` 
 
 
```syntaxsql  
-- Syntax for Parallel Data Warehouse  
  
ALTER CERTIFICATE certificate_name   
{  
      REMOVE PRIVATE KEY  
    | WITH PRIVATE KEY (   
        FILE = '<path_to_private_key>',  
        DECRYPTION BY PASSWORD = '<key password>' )
}  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *certificate_name*  
 Is the unique name by which the certificate is known in the database.  
  
 REMOVE PRIVATE KEY  
 Specifies that the private key should no longer be maintained inside the database.  
  
 WITH PRIVATE KEY
 Specifies that the private key of the certificate is loaded into SQL Server.

 FILE ='*path_to_private_key*'  
 Specifies the complete path, including file name, to the private key. This parameter can be a local path or a UNC path to a network location. This file will be accessed within the security context of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service account. When you use this option, make sure the service account has access to the specified file.
 
 If only a file name is specified, the file is saved in the default user data folder for the instance. This folder might (or might not) be the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA folder. For SQL Server Express LocalDB, the default user data folder for the instance is the path specified by the `%USERPROFILE%` environment variable for the account that created the instance.  
  
 BINARY ='*private_key_bits*'  
 **Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.  
  
 Private key bits specified as binary constant. These bits can be in encrypted form. If encrypted, the user must provide a decryption password. Password policy checks are not performed on this password. The private key bits should be in a PVK file format.  
  
 DECRYPTION BY PASSWORD ='*current_password*'  
 Specifies the password that is required to decrypt the private key.  
  
 ENCRYPTION BY PASSWORD ='*new_password*'  
 Specifies the password used to encrypt the private key of the certificate in the database. *new_password* must meet the Windows password policy requirements of the computer that is running the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For more information, see [Password Policy](../../relational-databases/security/password-policy.md).  
  
 ACTIVE FOR BEGIN_DIALOG **=** { ON | OFF }  
 Makes the certificate available to the initiator of a [!INCLUDE[ssSB](../../includes/sssb-md.md)] dialog conversation.  
  
## Remarks  
 The private key must correspond to the public key specified by *certificate_name*.  
  
 The DECRYPTION BY PASSWORD clause can be omitted if the password in the file is protected with a null password.  
  
 When the private key of a certificate that already exists in the database is imported, the private key will be automatically protected by the database master key. To protect the private key with a password, use the ENCRYPTION BY PASSWORD clause.  
  
 The REMOVE PRIVATE KEY option will delete the private key of the certificate from the database. You can remove the private key when the certificate will be used to verify signatures or in [!INCLUDE[ssSB](../../includes/sssb-md.md)] scenarios that do not require a private key. Do not remove the private key of a certificate that protects a symmetric key. The private key will need to be restored in order to sign any additional modules or strings that should be verified with the certificate, or to decrypt a value that has been encrypted with the certificate.   
  
 You do not have to specify a decryption password when the private key is encrypted by using the database master key.  
 
 To change the password used for encrypting the private key, do not specify either the FILE or BINARY clauses.
  
> [!IMPORTANT]  
>  Always make an archival copy of a private key before removing it from a database. For more information, see [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md) and [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md).  
  
 The WITH PRIVATE KEY option is not available in a contained database.  
  
## Permissions  
 Requires ALTER permission on the certificate.  
  
## Examples  
  
### A. Removing the private key of a certificate  
  
```sql  
ALTER CERTIFICATE Shipping04   
    REMOVE PRIVATE KEY;  
GO  
```  
  
### B. Changing the password that is used to encrypt the private key  
  
```sql  
ALTER CERTIFICATE Shipping11   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hkjdskghFDGGG4%',  
    ENCRYPTION BY PASSWORD = '34958tosdgfkh##38');  
GO  
```  
  
### C. Importing a private key for a certificate that is already present in the database  
  
```sql  
ALTER CERTIFICATE Shipping13   
    WITH PRIVATE KEY (FILE = 'c:\importedkeys\Shipping13',  
    DECRYPTION BY PASSWORD = 'GDFLKl8^^GGG4000%');  
GO  
```  
  
### D. Changing the protection of the private key from a password to the database master key  
  
```sql  
ALTER CERTIFICATE Shipping15   
    WITH PRIVATE KEY (DECRYPTION BY PASSWORD = '95hk000eEnvjkjy#F%');  
GO  
```  
  
## See Also  
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)  
 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)  
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  

