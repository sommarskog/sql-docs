---
title: "Subscriber Properties"
description: "Subscriber Properties"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.configdistwizard.subscribers.f1"
helpviewer_keywords:
  - "Subscriber Properties dialog box"
monikerRange: "=azuresqldb-current||>=sql-server-2016"
---
# Subscriber Properties
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  The **Subscriber Properties** dialog box contains information relevant to Subscribers running versions of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] before [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
## Options  
 **Agent Connection to the Subscriber**  
 The context under which the Distribution Agent and Merge Agent connect from the Distributor to the Subscriber This applies only to versions before [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Select **Impersonate agent process account** to make connections to the Subscriber using the context of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent account at the Distributor, or specify **SQL Server Authentication**, and then enter a value for **Login** and **Password**. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recommends that you select **Impersonate agent process account**.  
  
 For [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] and later versions, connection information is specified for each subscription in the New Subscription Wizard and can be changed in the **Subscription Properties** dialog box.  
  
 **Default Agent Schedules**  
 The default schedule used in the New Subscription Wizard for Subscribers running versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] before [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 **Miscellaneous**  
 Includes information on the Subscriber and Subscriber type.  
  
## See Also  
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
