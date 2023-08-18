---
title: "sp_changedistpublisher (Transact-SQL)"
description: "sp_changedistpublisher (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_changedistpublisher_TSQL"
  - "sp_changedistpublisher"
helpviewer_keywords:
  - "sp_changedistpublisher"
dev_langs:
  - "TSQL"
---
# sp_changedistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Changes the properties of the distribution Publisher. This stored procedure is executed at the Distributor on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the Publisher name. *publisher* is **sysname**, with no default.  
  
`[ @property = ] 'property'`
 Is a property to change for the given Publisher. *property* is **sysname** and can be one of these values.  
  
`[ @value = ] 'value'`
 Is the value for the given property. *value* is **nvarchar(255)**, with a default of NULL.  
  

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 This table describes the properties of Publishers and the values for those properties.  
  
|Property|Values|Description|  
|--------------|------------|-----------------|  
|**active**|**true**|Activates the Publisher.|  
||**false**|Deactivates the publisher|  
|**distribution_db**||Name of the distribution database.|  
|**login**||Login name.|  
|**password**||Strong password for the supplied login.|  
|**security_mode**|**1**|Use Windows Authentication when connecting to the Publisher. *This cannot be changed for a non-*[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publisher.*|  
||**0**|Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication when connecting to the Publisher. *This can't be changed for a non-*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publisher.*|  
|**working_directory**||Working directory used to store data and schema files for the publication.|  
|NULL (default)||All available *property* options are printed.| 
|**storage_connection_string**| Access key | The access key for the working directory when the database is Azure SQL Managed Instance. 
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_changedistpublisher** is used in all types of replication.  

 If you're changing the **working_directory** property and the **storage_connection_string** property has to be updated, execute the stored procedure separately by updating the **working_directory** property followed by updating the **storage_connection_string** property or visa-versa.
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_changedistpublisher**.  
  
## See Also  
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
