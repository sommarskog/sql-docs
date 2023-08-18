---
title: "Validate partition information (Merge)"
description: Describes how to validate partition information for a Merge Subscriber in SQL Server.
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "merge replication data validation [SQL Server replication], partitions"
  - "parameterized filters [SQL Server replication], validating partition information"
  - "validating partition information"
---
# Validate Partition Information for a Merge Subscriber
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  When you define a parameterized row filter for a merge publication, you use a function that references Subscriber information, such as the Subscriber's login name. By default, replication validates Subscriber information based on that function before each synchronization and whenever a snapshot is applied at the Subscriber. The validation process ensures that data is partitioned correctly for each Subscriber. Validation behavior is controlled by the **validate_subscriber_info** publication property, which can be changed using [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) or on the **Subscription Options** page of the **Publication Properties** dialog box. For more information about changing publication properties, see [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
## How Partition Validation Works  
 When a publication is filtered, for example, using the function **SUSER_SNAME()**, the Merge Agent applies the initial snapshot to each Subscriber based on data that is valid for the **SUSER_SNAME()** expression.  
  
 If validation is enabled, when the Subscriber reconnects to the Publisher for the next synchronization, the Merge Agent validates the information at the Subscriber and ensures that each Subscriber's partition is the same as the one received in the initial snapshot. For each subsequent merge or snapshot application, the Merge Agent validates each Subscriber's partition.  
  
 If the Merge Agent detects that the function used in the filtering expression returns a different value than it did at the initial snapshot, the merge or snapshot application fails, and that Subscriber's subscription might require reinitialization. Reinitialization might be necessary to prevent problems that can arise if the merge settings of a Subscriber are changed, but it might be sufficient to change information at the Subscriber, such as the login name, back to the value used at the time of the original snapshot.  
  
 When the Merge Agent validates a partition, in addition to validating the partition against the values returned by any functions used in filtering expressions, the agent also checks whether the snapshot was generated prior to changes that invalidate it, such as metadata cleanup operations or schema changes. If a partitioned snapshot is too old, the Merge Agent will return an error and you must regenerate a partitioned snapshot for that Subscriber based on a current regular snapshot.  
  
## See Also  
 [Replication Administration FAQ](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.yml)   
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [Reinitialize Subscriptions](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
