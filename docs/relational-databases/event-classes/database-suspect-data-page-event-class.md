---
title: "Database Suspect Data Page Event Class"
description: "Database Suspect Data Page Event Class"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: reference
helpviewer_keywords:
  - "event notifications [SQL Server], database mirroring"
  - "suspect_pages system table"
  - "database mirroring [SQL Server], event notifications"
  - "Database Suspect Data Page event class"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Database Suspect Data Page Event Class
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  The **Database Suspect Data Page** event class indicates when a page is added to the [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) table in [msdb](../../relational-databases/databases/msdb-database.md). Include this event class in traces that are monitoring the occurrence of suspect pages.  
  
> [!NOTE]  
>  This event is issued asynchronously from the insertion of a corresponding row into the **suspect_pages** table. Therefore, a job listening on this event might not find the corresponding **suspect_pages** entry immediately.  
  
 When the **Database Suspect Data Page** event class is included in a trace the relative overhead is low. The overhead might be greater if the number of suspect pages increases, for example, if a disk drive is experiencing problems.  
  
## Database Suspect Data Page Event Class Data Columns  
  
|Data Column Name|Data Type|Description|Column ID|Filterable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|ID of the database for which the suspect page event has been raised. This is the same as the **database_id** column of the **suspect_pages** table.|3|Yes|  
|**EventClass**|**int**|The type of the event is 213.|27|No|  
|**EventSequence**|**int**|Sequence of event class in batch.|51|No|  
|**SPID**|**int**|ID of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] task that encountered the suspect page.|12|Yes|  
|**StartTime**|**datetime**|Time that the event occurred.|14|Yes|  
|**ObjectID**|**int**|ID of the database file that contains the suspect page. This is the same as the **file_id** column of the **suspect_pages** table.|22|Yes|  
|**ObjectID2**|**int**|ID of the suspect page in the file. This is the same as the **page_id** column of the **suspect_pages** table.|56|Yes|  
|**Error**|**int**|Type of error that was encountered . This value is the same as the **event_type** value for the page in the **suspect_pages** table.|31|Yes|  
  
## See Also  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Manage the suspect_pages Table &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
