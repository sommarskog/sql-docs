---
title: "Subscriber Types"
description: "Subscriber Types"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.rep.newpubwizard.subscribertypes.f1"
monikerRange: "=azuresqldb-current||>=sql-server-2016"
---
# Subscriber Types
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  Merge replication allows you to specify the types of Subscribers that a publication must support. Selecting Subscriber types sets the *publication compatibility level*, which determines which features can be used by a publication.  
  
 After a publication snapshot is created, the publication compatibility level can be increased (made more restrictive) on the **General** page of the **Publication Properties** dialog box; the compatibility level cannot be decreased.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## Options  
 Select each Subscriber type that this publication must support.  
  
 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]  
 The publication can use all features.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 The publication requires snapshot files to be in character format (this is handled automatically by the Snapshot Agent). [!INCLUDE[ssEW](../../includes/ssew-md.md)] also has a number of restrictions not related to compatibility level.  
  
 If this option is selected, the Web synchronization option is enabled for the publication. For more information about Web synchronization, see [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## See Also  
 [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
