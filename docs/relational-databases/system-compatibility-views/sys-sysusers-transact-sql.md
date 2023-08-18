---
title: "sys.sysusers (Transact-SQL)"
description: "sys.sysusers (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.sysusers"
  - "sys.sysusers_TSQL"
  - "sysusers_TSQL"
  - "sysusers"
helpviewer_keywords:
  - "sysusers system table"
  - "sys.sysusers compatibility view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# sys.sysusers (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Contains one row for each [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows user, Windows group, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] user, or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] role in the database.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**uid**|**smallint**|User ID, unique in this database.<br /><br /> 1 = Database owner<br /><br /> Overflows or returns NULL if the number of users and roles exceeds 32,767.|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|User name or group name, unique in this database.|  
|**sid**|**varbinary(85)**|Security identifier for this entry.|  
|**roles**|**varbinary(2048)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|Date the account was added.|  
|**updatedate**|**datetime**|Date the account was last changed.|  
|**altuid**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Overflows or returns NULL if the number of users and roles exceeds 32,767.|  
|**password**|**varbinary(256)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**gid**|**smallint**|Group ID to which this user belongs. If **uid** is the same as **gid**, this entry defines a group. Overflows or returns NULL if the combined number of groups and users exceeds 32,767.|  
|**environ**|**varchar(255)**|Reserved.|  
|**hasdbaccess**|**int**|1 = Account has database access.|  
|**islogin**|**int**|1 = Account is a Windows group, Windows user, or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] user with a login account.|  
|**isntname**|**int**|1 = Account is a Windows group or Windows user.|  
|**isntgroup**|**int**|1 = Account is a Windows group.|  
|**isntuser**|**int**|1 = Account is a Windows user.|  
|**issqluser**|**int**|1 = Account is a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] user.|  
|**isaliased**|**int**|1 = Account is aliased to another user.|  
|**issqlrole**|**int**|1 = Account is a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] role.|  
|**isapprole**|**int**|1 = Account is an application role.|  
  
## See Also  
 [Mapping System Tables to System Views &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Compatibility Views &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
