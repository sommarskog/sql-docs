---
title: "MSSQLSERVER_21893"
description: "MSSQLSERVER_21893"
author: MashaMSFT
ms.author: mathoma
ms.date: "04/04/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: "reference"
helpviewer_keywords:
  - "21893 (Database Engine error)"
---
# MSSQLSERVER_21893
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## Details  
  
| Attribute | Value |  
| :-------- | :---- |  
|Product Name|SQL Server|  
|Event ID|21893|  
|Event Source|MSSQLSERVER|  
|Component|SQLEngine|  
|Symbolic Name|SQLErrorNum21893|  
|Message Text|The subscribers ( %s ) of original publisher '%s' do not appear as remote servers at redirected publisher '%s'. Run **sp_addlinkedserver** at the redirected publisher to add these subscribers as remote servers.|  
  
## Explanation  
**sp_validate_redirected_publisher** uses the subscription metadata tables of the publisher database at the remote server to identify its associated subscribers and verifies that there are associated entries in master.dbo.sysservers for the subscribers. This error is returned if any of the identified subscribers are not present.  
  
This error is not considered a fatal error. Agents encountering this error will log the error as informational but will not terminate, since a failure to have appropriate subscriber entries at the new publisher has limited impact on replication. Without an appropriate entry for a subscriber in sysservers, some subscription management activities may fail when executed through [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. However, these same activities can be successfully performed by executing the management stored procedures explicitly.  
  
## User Action  
Run **sp_addlinkedserver** at the redirected publisher for each of the identified subscribers to add them as remote servers. Then, run **sp_serveroption** to set the subscriber bit for the server.  
  
