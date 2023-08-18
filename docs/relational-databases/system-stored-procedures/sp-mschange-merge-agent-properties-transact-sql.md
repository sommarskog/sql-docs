---
title: "sp_MSchange_merge_agent_properties (Transact-SQL)"
description: "sp_MSchange_merge_agent_properties (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_MSchange_merge_agent_properties_TSQL"
  - "sp_MSchange_merge_agent_properties"
helpviewer_keywords:
  - "sp_MSchange_merge_agent_properties"
dev_langs:
  - "TSQL"
---
# sp_MSchange_merge_agent_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Changes the properties of a Merge Agent job that runs at a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] or later version Distributor. This stored procedure is used to change properties when the Publisher runs on an instance of [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. This stored procedure is executed at the Distributor on the distribution database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_MSchange_merge_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the name of the Publisher. *publisher* is **sysname**, with no default.  
  
`[ @publisher_db = ] 'publisher_db'`
 Is the name of the publication database. *publisher_db* is **sysname**, with no default.  
  
`[ @publication = ] 'publication'`
 Is the name of the publication. *publication* is **sysname**, with no default.  
  
`[ @subscriber = ] 'subscriber'`
 Is the name of the Subscriber. *subscriber* is **sysname**, with no default.  
  
`[ @subscriber_db = ] 'subscriber_db'`
 Is the name of the subscription database. *subscriber_db* is **sysname**, with no default.  
  
`[ @property = ] 'property'`
 Is the publication property to change. *property* is **sysname**, with no default.  
  
`[ @value = ] 'value'`
 Is the new property value. *value* is **nvarchar(524)**, with a default of NULL.  
  
 This table describes the properties of the Merge Agent job that can be changed and restrictions on the values for those properties.  
  
|Property|Value|Description|  
|--------------|-----------|-----------------|  
|**description**||A brief description of the subscription.|  
|**merge_job_login**||Login for the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows account under which the agent runs.|  
|**merge_job_password**||Password for the Windows account under which the agent job runs.|  
|**publisher_login**||Login to use when connecting to a Publisher to synchronize the subscription.|  
|**publisher_password**||Publisher password.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**publisher_security_mode**|**1**|Windows Authentication.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.|  
|**subscriber_login**||Login to use when connecting to a Subscriber to synchronize the subscription.|  
|**subscriber_password**||Subscriber password.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_security_mode**|**1**|Windows Authentication.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.|  
  
> [!NOTE]  
>  After changing an agent login or password, you must stop and restart the agent before the change takes effect.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_MSchange_merge_agent_properties** is used in merge replication.  
  
 When the Publisher runs on an instance of [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] or later version, you should use [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) to change properties of a Merge Agent job that synchronizes a push subscription that runs at the Distributor.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role at the Distributor can execute **sp_MSchange_merge_agent_properties**.  
  
## See Also  
 [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)  
  
  
