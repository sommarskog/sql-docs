---
title: "sp_copymergesnapshot (Transact-SQL)"
description: "sp_copymergesnapshot (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_copymergesnapshot"
  - "sp_copymergesnapshot_TSQL"
helpviewer_keywords:
  - "sp_copymergesnapshot"
dev_langs:
  - "TSQL"
---
# sp_copymergesnapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Copies the snapshot folder of the specified publication to the folder listed in the **\@destination_folder**. This stored procedure is executed at the Publisher on the publication database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the name of the publication whose snapshot contents are to be copied. *publication* is **sysname**, with no default.  
  
`[ @destination_folder = ] 'destination_folder'`
 Is the name of the folder where the contents of the publication snapshot is to be copied. *destination_folder*is **nvarchar(255)**, with no default. The *destination_folder* can be an alternate location such as on another server, on a network drive, or on removable media (such as CD-ROMs or removable disks).  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_copymergesnapshot** is used in merge replication. Subscribers running [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] version 7.0 and earlier cannot use the alternate snapshot location.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or **db_owner** fixed database role can execute **sp_copymergesnapshot**.  
  
## See Also  
 [Alternate Snapshot Folder Locations](../../relational-databases/replication/snapshot-options.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
