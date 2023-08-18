---
title: "Interactive Conflict Resolution"
description: "Advanced Merge Replication Conflict - Interactive Resolution"
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "interactive conflict resolution [SQL Server replication]"
  - "interactive resolver [SQL Server replication]"
  - "articles [SQL Server replication], conflict resolution"
  - "conflict resolution [SQL Server replication], merge replication"
---
# Advanced Merge Replication Conflict - Interactive Resolution
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] replication provides an Interactive Resolver, which allows you to resolve conflicts manually during on-demand synchronization in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows Synchronization Manager. Activated at run time, the Interactive Resolver is a graphical interface that displays data for each conflicting row, and provides options for viewing and editing the conflict data, and resolving each conflict individually.  
  
 The Interactive Resolver resembles the Conflict Viewer. However, the Conflict Viewer displays the results of conflicts that are already resolved after merge synchronization, and the Interactive Resolver displays each conflict prior to resolution, allowing you to determine the outcome of each conflict during merge synchronization. Someone should be available to monitor the Interactive Resolver when a conflict occurs.  
  
> [!NOTE]  
>  Interactive Resolution requires Windows Synchronization Manager. If a synchronization is performed outside of Windows Synchronization Manager (as a scheduled synchronization or an on demand synchronization in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] or Replication Monitor), conflicts are resolved automatically without user intervention, according to the resolver specified for the article. Conflicts that involve logical records are not displayed in the Interactive Resolver. To view information about these conflicts, use replication stored procedures. For more information, see [View Conflict Information for Merge Publications &#40;Replication Transact-SQL Programming&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md).  
  
## Article Resolvers and the Interactive Resolver  
 Conflict resolvers (either the default resolver, a business logic handler, or a custom resolver) are assigned to specific articles when a publication is created, and use a set of rules to determine which set of data should be used when conflicting row data is entered. The Interactive Resolver is not a separate conflict resolver with rules for determining conflict winners and losers, but a tool used in conjunction with default and custom resolvers. The article resolver still determines the winning and losing row, but the Interactive Resolver allows user intervention to accept, reject, or modify the results.  
  
 To use the Interactive Resolver, interactive resolution must be enabled for each article and subscription that requires it. After it is enabled for one or more articles and subscriptions, the Interactive Resolver is used when a conflict is detected during merge synchronization.  
  
 To use the Interactive Resolver, see [Specify Merge Replication options](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) and [Synchronize a Subscription Using Windows Synchronization Manager &#40;Windows Synchronization Manager&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## See Also  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
