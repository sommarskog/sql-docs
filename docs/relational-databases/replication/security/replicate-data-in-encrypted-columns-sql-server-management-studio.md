---
title: "Replicate encrypted columns (SSMS)"
description: Learn how to replicate data in encrypted columns using SQL Server Management Studio (SSMS).
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "encryption [SQL Server], replicating data"
  - "encryption [SQL Server replication]"
  - "publishing [SQL Server replication], encrypted columns"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# Replicate Data in Encrypted Columns (SQL Server Management Studio)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Replication enables you to publish encrypted column data. To decrypt and use this data at the Subscriber, the key that was used to encrypt the data at the Publisher must also be present on the Subscriber. Replication does not provide a secure mechanism to transport encryption keys. You must manually re-create the encryption key at the Subscriber. This topic shows you how to encrypt a column at the Publisher and make sure that the encryption key is available at the Subscriber.  
  
 The basic steps are as follows:  
  
1.  Create the symmetric key at the Publisher.  
  
2.  Encrypt column data with the symmetric key.  
  
3.  Publish the table with the encrypted column.  
  
4.  Subscribe to the publication.  
  
5.  Initialize the subscription.  
  
6.  Recreate the symmetric key at the Subscriber using same values for ALGORITHM, KEY_SOURCE, and IDENTITY_VALUE as in step 1.  
  
7.  Access the encrypted column data.  

> [!NOTE]  
>  You should use a symmetric key to encrypt column data. The symmetric key itself can be secured by different means at the Publisher and Subscriber.  
  
### To create and replicate encrypted column data  
  
1.  At the Publisher, execute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md).  
  
    > [!IMPORTANT]  
    >  The value of KEY_SOURCE is valuable data that can be used to re-create the symmetric key and decrypt data. KEY_SOURCE must always be stored and transported securely.  
  
2.  Execute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) to open the new key.  
  
3.  Use the [EncryptByKey](../../../t-sql/functions/encryptbykey-transact-sql.md) function to encrypt column data at the Publisher.  
  
4.  Execute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) to close the key.  
  
5.  Publish the table that contains the encrypted column. For more information, see [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  Subscribe to the publication. For more information, see [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md) or [Create a Push Subscription](../../../relational-databases/replication/create-a-push-subscription.md).  
  
7.  Initialize the subscription. For more information, see [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
8.  At the Subscriber, execute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md) using the same values for ALGORITHM, KEY_SOURCE, and IDENTITY_VALUE as in step 1. You can specify a different value for ENCRYPTION BY.  
  
    > [!IMPORTANT]  
    >  The value of KEY_SOURCE is valuable data that can be used to re-create the symmetric key and decrypt data. KEY_SOURCE must always be stored and transported securely.  
  
9. Execute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) to open the new key.  
  
10. Use the [DecryptByKey](../../../t-sql/functions/decryptbykey-transact-sql.md) function to decrypt replicated data at the Subscriber.  
  
11. Execute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) to close the key.  
  
## Examples

### A. Create keys in the publication database
 This example creates a symmetric key, a certificate that is used to help secure the symmetric key, and a master key. These keys are created in the publication database. They are then used to create an encrypted column (EncryptedCreditCardApprovalCode) in the `SalesOrderHeader` table. This column is published in the AdvWorksSalesOrdersMerge publication instead of the unencrypted CreditCardApprovalCode column. When possible, prompt users to enter security credentials at runtime. If you must store credentials in a script file, you must secure the file to prevent unauthorized access.  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_1.sql)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_2.sql)]  
  
### B. Create keys in the subscription database
 This example recreates the same symmetric key in the subscription database using the same values for ALGORITHM, KEY_SOURCE, and IDENTITY_VALUE from the first example. This example assumes that you have already initialized a subscription to the AdvWorksSalesOrdersMerge publication to replicate the encrypted column. When possible, prompt users to enter security credentials at runtime. If you must store credentials in a script file, you must secure the file during storage and transport to prevent unauthorized access.  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_3.sql)]  
  
## See Also  
 [View and modify replication security settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Create Identical Symmetric Keys on Two Servers](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
