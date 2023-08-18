---
title: "sp_validatemergepublication (Transact-SQL)"
description: "sp_validatemergepublication (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_validatemergepublication"
  - "sp_validatemergepublication_TSQL"
helpviewer_keywords:
  - "sp_validatemergepublication"
dev_langs:
  - "TSQL"
---
# sp_validatemergepublication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Performs a publication-wide validation for which all subscriptions (push, pull, and anonymous) will be validated once. This stored procedure is executed at the Publisher on the publication database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_validatemergepublication [@publication=] 'publication'  
        , [ @level = ] level  
```  
  
## Arguments  
 [**\@publication=**] **'***publication***'**  
 Is the name of the publication. *publication* is **sysname**, with no default.  
  
`[ @level = ] level`
 Is the type of validation to perform. *level* is **tinyint**, with no default. Level can be one of these values.  
  
|Level value|Description|  
|-----------------|-----------------|  
|**1**|Rowcount-only validation.|  
|**2**|Rowcount and checksum validation. For [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Subscribers, this is automatically set to **3**.|  
|**3**|This is the recommended value.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_validatemergepublication** is used in merge replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_validatemergepublication**.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Validate Replicated Data](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_validatemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)  
  
  
