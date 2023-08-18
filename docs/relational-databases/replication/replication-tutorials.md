---
title: "Replication tutorials"
description: Use these tutorials to help prepare your server for replication in SQL Server, and then learn to configure both transactional and merge replication.
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "04/09/2018"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "tutorials [SQL Server replication]"
  - "walkthroughs [SQL Server replication]"
  - "replication [SQL Server], tutorials"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# Replication tutorials
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
Replication is a powerful solution for moving data, or subsets of data, between servers. You can replicate data between servers that are fully connected by using transactional replication. You can also replicate data between servers and clients that are intermittently connected by using merge replication. In this article, you will find tutorials that help prepare your server for replication, and then teach you to configure both transactional and merge replication. 
  
In the replication tutorials, "publisher" refers to the server that contains the source data that's being replicated. "Subscriber" refers to the destination server. The publisher and subscriber might share the same instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], but it is not a requirement. For more information, see the [overview of the replication publishing model](../../relational-databases/replication/publish/replication-publishing-model-overview.md).  

These tutorials use NODE1\SQL2016 as the publisher and distributor. They use NODE2\SQL2016 as the subscriber. 
  
> [!NOTE]  
> Most of the tasks shown in these tutorials can be performed programmatically. For more information, see the [replication developer documentation](../../relational-databases/replication/concepts/replication-developer-documentation.md).  
  
## Replication tutorials  
[Tutorial: Prepare SQL Server for replication (publisher, distributor, subscriber)](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
Learn how to prepare servers so that replication can be run with least privileges. You must complete this tutorial before the other replication tutorials.  
  
[Tutorial: Configure replication between two fully connected servers (transactional)](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

Learn how to configure transactional replication to replicate data between fully connected servers. This tutorial also includes some basic error troubleshooting methodology. 

  
[Tutorial: Configure replication between a server and mobile clients (merge)](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

Learn how to configure merge replication to exchange data between a server and one or more clients that are only occasionally connected.  
  
## See also  
[View and modify replication security settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) 

[Transactional replication overview](./transactional/transactional-replication.md) 

[Merge replication overview](./merge/merge-replication.md)

