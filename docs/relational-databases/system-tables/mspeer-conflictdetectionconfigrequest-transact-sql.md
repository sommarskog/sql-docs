---
title: "MSpeer_conflictdetectionconfigrequest (T-SQL)"
description: Describes the  MSPeer_conflictdetectionconfigurerequest  stored procedure used to track topology wide configuration requests for a  Peer-to-Peer Publication.
author: VanMSFT
ms.author: vanto
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSpeer_conflictdetectionconfigrequest_TSQL"
  - "MSpeer_conflictdetectionconfigrequest"
helpviewer_keywords:
  - "MSpeer_conflictdetectionconfigurerequest"
dev_langs:
  - "TSQL"
---
# MSpeer_conflictdetectionconfigrequest (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Used in peer-to-peer replication to track topology wide configuration requests for a publication. This table is stored in the publication database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|Identifies a conflict configuration request. The request_id column in [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md) uses this value.|  
|publication|**sysname**|Name of the publication from which the conflict configuration request originated.|  
|sent_date|**datetime**|Date and time that the conflict configuration request was initiated.|  
|timeout|**int**|Amount of time that a procedure should wait for all peers to return conflict information.|  
|modified_date|**datetime**|Date and time that a phase was completed.|  
|progress_phase|**nvarchar(32)**|Identifies the current phase of processing, by using one of the following values:<br /><br /> Started<br /><br /> Exploring topology<br /><br /> Collecting status<br /><br /> Status collected|  
|phase_timed_out|**bit**|Indicates whether the current phase has timed out.|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
