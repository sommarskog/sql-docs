---
title: "sp_replmonitorchangepublicationthreshold (T-SQL)"
description: Describes the sp_replmonitorchangepublicationthreshold stored procedure which changes the monitoring threshold metric for a publication.
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_replmonitorchangepublicationthreshold_TSQL"
  - "sp_replmonitorchangepublicationthreshold"
helpviewer_keywords:
  - "sp_replmonitorchangepublicationthreshold"
dev_langs:
  - "TSQL"
---
# sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Changes the monitoring threshold metric for a publication. This stored procedure, which is used to monitor replication, is executed at the Distributor on the distribution database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## Arguments  
`[ @publisher = ] 'publisher'`
 Is the name of the Publisher. *publisher* is **sysname**, with no default.  
  
`[ @publisher_db = ] 'publisher_db'`
 Is the name of the published database. *publisher_db* is **sysname**, with no default.  
  
`[ @publication = ] 'publication'`
 Is the name of the publication for which the monitoring threshold attributes are being changed. *publication* is **sysname**, with no default.  
  
`[ @publication_type = ] publication_type`
 If the type of publication. *publication_type* is **int**, and can be one of these values.  
  
|Value|Description|  
|-----------|-----------------|  
|**0**|Transactional publication.|  
|**1**|Snapshot publication.|  
|**2**|Merge publication.|  
|NULL (default)|Replication attempts to determine the publication type.|  
  
`[ @metric_id = ] metric_id`
 Is the ID of the publication threshold metric being changed. *metric_id* is **int**, with a default value of NULL and can be one of these values.  
  
|Value|Metric Name|  
|-----------|-----------------|  
|**1**|**expiration** - monitors for imminent expiration of subscriptions to transactional publications.|  
|**2**|**latency** - monitors for the performance of subscriptions to transactional publications.|  
|**4**|**mergeexpiration** - monitors for imminent expiration of subscriptions to merge publications.|  
|**5**|**mergeslowrunduration** - monitors the duration of merge synchronizations over low-bandwidth (dial-up) connections.|  
|**6**|**mergefastrunduration** - monitors the duration of merge synchronizations over high-bandwidth local area network (LAN) connections.|  
|**7**|**mergefastrunspeed** - monitors the synchronization rate of merge synchronizations over high-bandwidth (LAN) connections.|  
|**8**|**mergeslowrunspeed** - monitors the synchronization rate of merge synchronizations over low-bandwidth (dial-up) connections.|  
  
 You must specify either *metric_id* or *thresholdmetricname*. If *thresholdmetricname* is specified, then *metric_id* should be NULL.  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'`
 Is the name of the publication threshold metric being changed. *thresholdmetricname* is **sysname**, with a default value of NULL. You must specify either *thresholdmetricname* or *metric_id*. If *metric_id* is specified, then *thresholdmetricname* should be NULL.  
  
`[ @value = ] value`
 Is the new value of the publication threshold metric. *value* is **int**, with a default value of NULL. If **null**, then the metric value is not updated.  
  
`[ @shouldalert = ] shouldalert`
 Is if an alert is generated when a publication threshold metric is reached. *shouldalert* is **bit**, with a default of NULL. A value of **1** means that an alert is generated, and a value of **0** means that an alert is not generated.  
  
`[ @mode = ] mode`
 Is if the publication threshold metric is enabled. *mode* is **tinyint**, with a default of **1**. A value of **1** means that monitoring of this metric is enabled, and a value of **2** means that monitoring of this metric is disabled.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_replmonitorchangepublicationthreshold** is used with all types of replication.  
  
## Permissions  
 Only members of the **db_owner** or **replmonitor** fixed database role in the distribution database can execute **sp_replmonitorchangepublicationthreshold**.  
  
## See Also  
 [Programmatically Monitor Replication](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
