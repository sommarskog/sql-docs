---
title: "Organize Jobs"
description: "Organize Jobs"
author: markingmyname
ms.author: maghan
ms.date: 01/19/2017
ms.service: sql
ms.subservice: ssms
ms.topic: conceptual
helpviewer_keywords:
  - "job category"
  - "organize jobs"
monikerRange: "= azuresqldb-mi-current || >= sql-server-2016"
---
# Organize Jobs
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> On [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), most, but not all SQL Server Agent features are currently supported. See [Azure SQL Managed Instance T-SQL differences from SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) for details.

Job categories help you organize your jobs for easy filtering and grouping. For example, you can organize all your database backup jobs in the Database Maintenance category. You can also create your own job categories.  
  
> [!WARNING]  
> Multiserver categories exist only on a master server. There is only one default job category available on a master server: [**Uncategorized (Multi-Server)**]. When a multiserver job is downloaded, its category is changed to **Jobs From MSX** at the target server.  
  
## Related Tasks  
  
|Description|Topic|  
|-|-|  
|Describes how to create a job category.|[Create a Job Category](../../ssms/agent/create-a-job-category.md)|  
|Describes how to delete a job category.|[Delete a Job Category](../../ssms/agent/delete-a-job-category.md)|  
|Describes how to assign a job to a job category.|[Assign a Job to a Job Category](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|Describes how to change the membership of a job category.|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|Describes how to list the category information.|[List Job Category Information](../../ssms/agent/list-job-category-information.md)|  
