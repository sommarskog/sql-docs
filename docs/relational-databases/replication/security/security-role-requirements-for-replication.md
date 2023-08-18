---
title: "Security Role Requirements for Replication"
description: Learn about the authentication level necessary for common replication setup tasks and for common replication maintenance tasks in SQL Server.
author: "MashaMSFT"
ms.author: "mathoma"
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "security [SQL Server replication], roles"
  - "roles [SQL Server], replication"
monikerRange: "=azuresqldb-mi-current||>=sql-server-2016"
---
# Security Role Requirements for Replication
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Replication restricts the specific actions that a user can perform based on the roles to which the user's login is mapped. Replication has granted certain permissions to the **sysadmin** fixed server role, the **db_owner** fixed database role, and the logins in the publication access list (PAL).  
  
## Security Role Requirements for Replication Setup  
 The following table summarizes the authentication level necessary for common replication setup tasks:  
  
|Setup task|Membership requirement|  
|----------------|----------------------------|  
|Enable a Distributor, Publisher, or Subscriber.|**sysadmin** server role on the Publisher.|  
|Enable a database for replication.|**sysadmin** server role on the Publisher.|  
|Create a publication.|**db_owner** database role on the publication database at the Publisher or **sysadmin** server role on the Publisher.|  
|View publication properties.|Member of the PAL at the Publisher, **db_owner** database role on the publication database at the Publisher, or **sysadmin** server role on the Publisher.|  
|Create a subscription.|**db_owner** database role on the publication database at the Publisher or **sysadmin** server role on the Publisher.<br /><br /> **db_owner** database role on the subscription database at the Subscriber or **sysadmin** server role on the Subscriber.|  
|Configure agent profiles.|**sysadmin** server role on the Distributor.|  
  
## Security Role Requirements for Replication Maintenance  
 The following table summarizes the authentication level necessary for common replication maintenance tasks:  
  
|Maintenance task|Membership requirement|  
|----------------------|----------------------------|  
|Modify or drop a Distributor, Publisher, or Subscriber.|**sysadmin** server role on the appropriate server.|  
|Modify or drop a publication.|**db_owner** database role on the publication database at the Publisher or **sysadmin** server role on the Publisher.|  
|Modify or drop a subscription at the Publisher.|**db_owner** database role on the publication database at the Publisher or **sysadmin** server role on the Publisher.|  
|Modify or drop a subscription at the Subscriber.|**db_owner** database role on the subscription database at the Subscriber or **sysadmin** server role on the Subscriber.|  
|Mark a subscription for reinitialization.|Push subscription: **db_owner** database role in the publication database at the Publisher or **sysadmin** server role on the Publisher.<br /><br /> Pull subscription: **db_owner** database role in the subscription database at the Subscriber or **sysadmin** server role on the Subscriber.|  
|View replication activity, errors, and history using Replication Monitor. A user cannot modify agent profiles, schedules, and so on, unless the user is a member of the **sysadmin** server role.|**replmonitor** database role on the distribution database at the Distributor or **sysadmin** server role on the Distributor.|  
|Maintain replication agents.|**db_owner** database role in the appropriate database or **sysadmin** server role on the appropriate server.<br /><br /> If the agent was created by a user in the **sysadmin** role, and a proxy account was not specified for the agent, the agent runs under the context of the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent account. In this case, a user in the **db_owner** role cannot modify the job associated with the agent.|  
|Start or stop a replication agent.|Owner of the agent job or **sysadmin** server role on the appropriate server.|  
  
## See Also  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [View and modify replication security settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
