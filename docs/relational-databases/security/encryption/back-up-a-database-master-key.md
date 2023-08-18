---
title: "Back up a database master key"
description: Learn how to back up a database master key in SQL Server by using Transact-SQL. This essential key encrypts other keys and certificates.
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
ms.date: "12/16/2021"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "database master key [SQL Server], exporting"
---

# Back up a database master key

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to back up a database master key in [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] by using [!INCLUDE[tsql](../../../includes/tsql-md.md)]. The database master key is used to encrypt other keys and certificates inside a database. If it's deleted or corrupted, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] may be unable to decrypt those keys, and the data encrypted using them will be effectively lost. For this reason, you should back up the database master key and store the backup in a secure off-site location.  
  
## Before you begin  
  
### Limitations and restrictions  
  
- The master key must be open and, therefore, decrypted before it's backed up. If it's encrypted with the service master key, the master key doesn't have to be explicitly opened. But if the master key is encrypted only with a password, it must be explicitly opened.  
  
- We recommend that you back up the master key as soon as it's created, and store the backup in a secure, off-site location.  
  
## Security  
  
### Permissions
Requires CONTROL permission on the database.  
  
## Using SQL Server Management Studio with Transact-SQL  
  
### To back up the database master key  
  
1. In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], connect to the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instance containing the database master key you wish to back up.  
  
2. Choose a password that will be used to encrypt the database master key on the backup medium. This password is subject to complexity checks.  
  
3. Obtain a removable backup medium for storing a copy of the backed-up key.  
  
4. Identify an NTFS directory in which to create the backup of the key. This is where you'll create the file specified in the next step. The directory should be protected with highly restrictive access control lists (ACLs).  
  
5. In **Object Explorer**, connect to an instance of [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
6. On the Standard bar, click **New Query**.  
  
7. Copy and paste the following example into the query window and click **Execute**.  
  
    ```sql
    -- Creates a backup of the "AdventureWorks2022" master key. Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2022;   
    GO  
    OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';   
  
    BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
        ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';   
    GO  
    ```  
  
    > [!NOTE]  
    > The file path to the key and the key's password (if it exists) will be different than what is indicated above. Please make sure that both are specific to your server and key set-up.  
  
8. Copy the file to the backup medium and verify the copy.  
  
9. Store the backup in a secure, off-site location.  

## See also

 For more information, see [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-master-key-transact-sql.md) and [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-master-key-transact-sql.md).  
