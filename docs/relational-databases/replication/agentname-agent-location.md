---
title: "&lt;AgentName&gt; Agent Location"
description: "&lt;AgentName&gt; Agent Location"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.newsubwizard.agentlocation.f1"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# &lt;AgentName&gt; Agent Location
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  The Merge Agent (for merge subscriptions) and the Distribution Agent (for transactional and snapshot subscriptions) run at the Distributor or at the Subscriber. If the agent runs at the Distributor, the subscription is referred to as a push subscription; if the agent runs at the Subscriber, it is referred to as a pull subscription. For more information about push and pull subscriptions, see [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md). All subscriptions created in this pass through the wizard will be of the selected type. To create subscriptions of both types, you must run the wizard twice.  
  
> [!NOTE]  
>  Subscription type cannot be changed after a subscription is created.  
  
## See Also  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
