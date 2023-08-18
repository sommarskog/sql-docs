---
title: "dbo.sysjobs (Transact-SQL)"
description: dbo.sysjobs (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "08/09/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sysjobs"
  - "sysjobs_TSQL"
  - "dbo.sysjobs"
  - "dbo.sysjobs_TSQL"
helpviewer_keywords:
  - "sysjobs system table"
dev_langs:
  - "TSQL"
---
# dbo.sysjobs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Stores the information for each scheduled job to be executed by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. This table is stored in the **msdb** database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Unique ID of the job.|  
|**originating_server_id**|**int**|ID of the server from which the job came.|  
|**name**|**sysname**|Name of the job.|  
|**enabled**|**tinyint**|Indicates whether the job is enabled to be executed.|  
|**description**|**nvarchar(512)**|Description for the job.|  
|**start_step_id**|**int**|ID of the step in the job where execution should begin.|  
|**category_id**|**int**|ID of the job category.|  
|**owner_sid**|**varbinary(85)**|Security identifier number (SID) of the job owner.|  
|**notify_level_eventlog**|**int**|**Bitmask** indicating under what circumstances a notification event should be logged to the Microsoft Windows application log:<br /><br /> **0** = Never<br /><br /> **1** = When the job succeeds<br /><br /> **2** = When the job fails<br /><br /> **3** = Whenever the job completes (regardless of the job outcome)|  
|**notify_level_email**|**int**|Bitmask indicating under what circumstances a notification e-mail should be sent when a job completes:<br /><br /> **0** = Never<br /><br /> **1** = When the job succeeds<br /><br /> **2** = When the job fails<br /><br /> **3** = Whenever the job completes (regardless of the job outcome)|  
|**notify_level_netsend**|**int**|Bitmask indicating under what circumstances a network message should be sent when a job completes:<br /><br /> **0** = Never<br /><br /> **1** = When the job succeeds<br /><br /> **2** = When the job fails<br /><br /> **3** = Whenever the job completes (regardless of the job outcome)|  
|**notify_level_page**|**int**|Bitmask indicating under what circumstances a page should be sent when a job completes:<br /><br /> **0** = Never<br /><br /> **1** = When the job succeeds<br /><br /> **2** = When the job fails<br /><br /> **3** = Whenever the job completes (regardless of the job outcome)|  
|**notify_email_operator_id**|**int**|E-mail name of the operator to notify.|  
|**notify_netsend_operator_id**|**int**|ID of the computer or user used when sending network messages.|  
|**notify_page_operator_id**|**int**|ID of the computer or user used when sending a page.|  
|**delete_level**|**int**|**Bitmask** indicating under what circumstances the job should be deleted when a job completes:<br /><br /> **0** = Never<br /><br /> **1** = When the job succeeds<br /><br /> **2** = When the job fails<br /><br /> **3** = Whenever the job completes (regardless of the job outcome)|  
|**date_created**|**datetime**|Date the job was created.|  
|**date_modified**|**datetime**|Date the job was last modified.|  
|**version_number**|**int**|Version of the job.|  
  
  
