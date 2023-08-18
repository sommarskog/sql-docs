---
title: "Enable initialization with backup (Transactional)"
description: Learn how to enable initialization from a backup for a Transactional Publication in SQL Server.
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/07/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "manual subscription initialization [SQL Server replication]"
  - "subscriptions [SQL Server replication], initializing"
  - "initializing subscriptions [SQL Server replication], without snapshots"
  - "transactional replication, backup and restore"
  - "backups [SQL Server replication], transactional replication"
---
# Enable Initialization with Backup for Transactional Publications
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  To initialize a subscription to a transactional publication from a backup, enable the publication to allow initialization from a backup, and then specify backup information when creating the subscription:  
  
-   Enable the publication on the **Subscription Options** page of the **Publication Properties - \<Publication>** dialog box. For more information about accessing this dialog box, see [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
-   Specify backup information with the stored procedure [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). For more information about the parameters required by **sp_addsubscription**, see [Initialize a Transactional Subscription from a Backup &#40;Replication Transact-SQL Programming&#41;](../../relational-databases/replication/initialize-a-transactional-subscription-from-a-backup.md).  
  
### To enable initialization with a backup  
  
1.  On the **Subscription Options** page of the **Publication Properties - \<Publication>** dialog box, select a value of **True** for the **Allow initialization from backup files** option.  
  
## See Also  
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
