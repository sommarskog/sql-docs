---
title: "sp_browsesnapshotfolder (Transact-SQL)"
description: "sp_browsesnapshotfolder (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_browsesnapshotfolder"
  - "sp_browsesnapshotfolder_TSQL"
helpviewer_keywords:
  - "sp_browsesnapshotfolder"
dev_langs:
  - "TSQL"
---
# sp_browsesnapshotfolder (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Returns the complete path for the latest snapshot generated for a publication. This stored procedure is executed at the Publisher on the publication database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the name of the publication that contains the article. *publication* is **sysname**, with no default.  
  
`[ @subscriber = ] 'subscriber'`
 Is the name of the Subscriber. *subscriber* is **sysname**, with a default of NULL.  
  
`[ @subscriber_db = ] 'subscriber_db'`
 Is the name of the subscription database. *subscriber_db* is **sysname**, with a default of NULL.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|Full path to the snapshot directory.|  
  
## Remarks  
 **sp_browsesnapshotfolder** is used in snapshot replication and transactional replication.  
  
 If the *subscriber* and *subscriber_db* fields are left NULL, the stored procedure returns the snapshot folder of the most recent snapshot it can find for the publication. If the *subscriber* and *subscriber_db* fields are specified, the stored procedure returns the snapshot folder for the specified subscription. If a snapshot has not been generated for the publication, an empty result set is returned.  
  
 If the publication is set up to generate snapshot files in both the Publisher working directory and Publisher snapshot folder, the result set contains two rows. The first row contains the publication snapshot folder and the second row contains the publisher working directory. **sp_browsesnapshotfolder** is useful for determining the directory where snapshot files are generated.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute **sp_browsesnapshotfolder**.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
