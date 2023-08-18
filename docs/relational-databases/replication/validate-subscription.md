---
title: "Validate Subscription"
description: "Validate Subscription"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.validate.validateandresynch.f1"
helpviewer_keywords:
  - "Validate Subscription dialog box"
monikerRange: "=azuresqldb-current||>=sql-server-2016"
---
# Validate Subscription
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Use the **Validate Subscription** dialog box to specify that a subscription to a merge publication should be validated the next time the Merge Agent for the subscription runs. The results of validation are displayed in Replication Monitor. For more information, see [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
 It is also possible to validate all subscriptions to a merge publication by right-clicking a publication in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] and clicking **Validate All Subscriptions**.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## Options  
 **Date of the last attempted validation**  
 The date of the last Merge Agent session that included subscription validation, whether or not that validation was successful.  
  
 **Date of the last successful validation**  
 The date of the last Merge Agent session that included a successful subscription validation.  
  
 **Validate this subscription**  
 Select to validate the subscription.  
  
 **Options**  
 Click to access the **Subscription Validation Options** dialog box, which allows you to specify whether to use row count validation or binary checksum validation.  
  
## See Also  
 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
