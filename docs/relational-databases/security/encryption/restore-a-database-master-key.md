---
title: "Restore a database master key"
description: Learn how to restore the database master key in SQL Server by using SQL Server Management Studio with Transact-SQL.
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
ms.date: "12/16/2021"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "database master key [SQL Server], importing"
---
# Restore a database master key
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to restore the database master key in [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)] by using [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## Before you begin  
  
### Limitations and restrictions  
  
- When the master key is restored, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] decrypts all the keys that are encrypted with the currently active master key, and then encrypts these keys with the restored master key. This resource-intensive operation should be scheduled during a period of low demand. If the current database master key isn't open or can't be opened, or if any of the keys that are encrypted by it cannot be decrypted, the restore operation fails.  
  
- If any one of the decryptions fails, the restore will fail. You can use the FORCE option to ignore errors, but this option will cause the loss of any data that cannot be decrypted.  
  
- If the master key was encrypted by the service master key, the restored master key will also be encrypted by the service master key.  
  
- If there's no master key in the current database, RESTORE MASTER KEY creates a master key. The new master key won't be automatically encrypted with the service master key.  
  
## Security  
  
### Permissions
Requires CONTROL permission on the database.  
  
## Using SQL Server Management Studio with Transact-SQL  
  
### To restore the database master key  
  
1. Retrieve a copy of the backed-up database master key, either from a physical backup medium or a directory on the local file system.  
  
2. In **Object Explorer**, connect to an instance of [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3. On the Standard bar, click **New Query**.  
  
4. Copy and paste the following example into the query window and click **Execute**.  

    ```sql
    -- Restores the database master key of the AdventureWorks2022 database.  
    USE AdventureWorks2022;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2022_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    > The file path to the key and the key's password (if it exists) will be different than what is indicated above. Please make sure that both are specific to your server and key set-up.  


## See also

- [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)  
