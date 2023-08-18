---
title: "BACKUP CERTIFICATE (Transact-SQL)"
description: BACKUP CERTIFICATE (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "05/24/2022"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "DUMP_CERTIFICATE_TSQL"
  - "BACKUP CERTIFICATE"
  - "sql13.swb.exportcertificate.f1"
  - "DUMP CERTIFICATE"
  - "BACKUP_CERTIFICATE_TSQL"
helpviewer_keywords:
  - "encryption [SQL Server], certificates"
  - "decryption [SQL Server], certificates"
  - "exporting certificates"
  - "certificates [SQL Server], exporting"
  - "BACKUP CERTIFICATE statement"
  - "backing up certificates [SQL Server]"
  - "decryption [SQL Server]"
  - "cryptography [SQL Server], certificates"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017"
---
# BACKUP CERTIFICATE (Transact-SQL)
[!INCLUDE [sql-asdbmi](../../includes/applies-to-version/sql-asdbmi.md)]

  Exports a certificate to a file.

> [!NOTE]
> In [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)], certificates with private keys can be backed up or restored directly to and from files or binary blobs using the public key pairs (PKCS) #12 or personal information exchange (PFX) format.
>
> The PKCS #12 or PFX format is a binary format for storing the server certificate, any intermediate certificates, and the private key in one file. PFX files usually have extensions such as `.pfx` and `.p12`. This makes it easier for customers to adhere to the current security best practice guidelines and compliance standards that prohibit RC4 encryption, by eliminating the need to use conversion tools such as PVKConverter (for the PVK or DER format).
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
-- Syntax for SQL Server  
  
BACKUP CERTIFICATE certname TO FILE = 'path_to_file'  
    [ WITH
      [FORMAT = 'PFX',]
      PRIVATE KEY   
      (   
        FILE = 'path_to_private_key_file' ,  
        ENCRYPTION BY PASSWORD = 'encryption_password'   
        [ , DECRYPTION BY PASSWORD = 'decryption_password' ]   
      )   
    ]  
```  
  
   
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
BACKUP CERTIFICATE certname TO FILE ='path_to_file'  
      WITH PRIVATE KEY   
      (   
        FILE ='path_to_private_key_file',  
        ENCRYPTION BY PASSWORD ='encryption_password'   
      )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *certname*  
 Is the name of the certificate to back up.

 TO FILE = '*path_to_file*'  
 Specifies the complete path, including file name, of the file in which the certificate is to be saved. This path can be a local path or a UNC path to a network location. If only a file name is specified, the file will be saved in the instance's default user data folder (which may or may not be the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA folder). For SQL Server Express LocalDB, the instance's default user data folder is the path specified by the `%USERPROFILE%` environment variable for the account that created the instance.  

 WITH FORMAT = *'PFX'*   
 **Applies to:** [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)] and later   
 Specifies exporting a certificate and its private key to a PFX file. This clause is optional.

 WITH PRIVATE KEY
 Specifies that the private key of the certificate is to be saved to a file. This clause is optional.

 FILE = '*path_to_private_key_file*'  
 Specifies the complete path, including file name, of the file in which the private key is to be saved. This path can be a local path or a UNC path to a network location. If only a file name is specified, the file will be saved in the instance's default user data folder (which may or may not be the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DATA folder). For SQL Server Express LocalDB, the instance's default user data folder is the path specified by the `%USERPROFILE%` environment variable for the account that created the instance.  

 ENCRYPTION BY PASSWORD = '*encryption_password*'  
 Is the password that is used to encrypt the private key before writing the key to the backup file. The password is subject to complexity checks.  
  
 DECRYPTION BY PASSWORD = '*decryption_password*'  
 Is the password that is used to decrypt the private key before backing up the key. This argument isn't necessary if the certificate is encrypted by the master key. 
  
## Remarks  
 If the private key is encrypted with a password in the database, the decryption password must be specified.  
  
 When you back up the private key to a file, encryption is required. The password used to protect the private key in the file isn't the same password that is used to encrypt the private key of the certificate in the database.  

 Private keys are saved in the PVK file format.

 To restore a backed-up certificate, with or without the private key, use the [CREATE CERTIFICATE](../../t-sql/statements/create-certificate-transact-sql.md) statement.
 
 To restore a private key to an existing certificate in the database, use the [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md) statement.
 
 When performing a backup, the files will be ACLd to the service account of the SQL Server instance. If you need to restore the certificate to a server running under a different account, you'll need to adjust the permissions on the files so that they're able to be read by the new account. 
  
## Permissions  
 Requires CONTROL permission on the certificate and knowledge of the password that is used to encrypt the private key. If only the public part of the certificate is backed up, this command requires some permission on the certificate and that the caller hasn't been denied VIEW permission on the certificate.  
  
## Examples  
  
### A. Exporting a certificate to a file  
 The following example exports a certificate to a file.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert';  
GO  
```  
  
### B. Exporting a certificate and a private key  
 In the following example, the private key of the certificate that is backed up will be encrypted with the password `997jkhUbhk$w4ez0876hKHJH5gh`.  
  
```sql
BACKUP CERTIFICATE sales05 TO FILE = 'c:\storedcerts\sales05cert'  
    WITH PRIVATE KEY ( FILE = 'c:\storedkeys\sales05key' ,   
    ENCRYPTION BY PASSWORD = '997jkhUbhk$w4ez0876hKHJH5gh' );  
GO  
```  
  
### C. Exporting a certificate that has an encrypted private key  
 In the following example, the private key of the certificate is encrypted in the database. The private key must be decrypted with the password `9875t6#6rfid7vble7r`. When the certificate is stored to the backup file, the private key will be encrypted with the password `9n34khUbhk$w4ecJH5gh`.  
  
```sql
BACKUP CERTIFICATE sales09 TO FILE = 'c:\storedcerts\sales09cert'   
    WITH PRIVATE KEY ( DECRYPTION BY PASSWORD = '9875t6#6rfid7vble7r' ,  
    FILE = 'c:\storedkeys\sales09key' ,   
    ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh' );  
GO  
```

### D. Export a certificate and its private key to a PFX file

```sql
BACKUP CERTIFICATE Shipping04 TO FILE = 'c:\storedcerts\shipping04cert.pfx'
WITH  
    FORMAT = 'PFX',  
    PRIVATE KEY ( 
ENCRYPTION BY PASSWORD = '9n34khUbhk$w4ecJH5gh',  
ALGORITHM = 'AES_256'
    )
```

## See also

 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)  
 [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md)  
 [CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)  
 [CERTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/certproperty-transact-sql.md)  
  
  
