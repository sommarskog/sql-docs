---
title: "Implement Jobs"
description: "Implement Jobs"
author: markingmyname
ms.author: maghan
ms.date: 01/19/2017
ms.service: sql
ms.subservice: ssms
ms.topic: conceptual
helpviewer_keywords:
  - "jobs [SQL Server Agent]"
  - "SQL Server Agent jobs"
  - "SQL Server Agent jobs, about jobs"
  - "jobs [SQL Server Agent], about jobs"
monikerRange: "= azuresqldb-mi-current || >= sql-server-2016"
---
# Implement Jobs
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> On [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), most, but not all SQL Server Agent features are currently supported. See [Azure SQL Managed Instance T-SQL differences from SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) for details.

You can use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent jobs to automate routine administrative tasks and run them on a recurring basis, making administration more efficient.  
  
A job is a specified series of operations performed sequentially by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A job can perform a wide range of activities, including running [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts, command-line applications, Microsoft ActiveX scripts, Integration Services packages, Analysis Services commands and queries, or Replication tasks. Jobs can run repetitive tasks or those that can be scheduled, and they can automatically notify users of job status by generating alerts, thereby greatly simplifying [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administration.  
  
You can run a job manually, or you can configure it to run according to a schedule or in response to alerts.  
  
## Related Tasks  
  
|Description|Topic|  
|-|-|   
|Contains information about creating jobs and assigning ownership.|[Create Jobs](../../ssms/agent/create-jobs.md)|  
|Contains information about organizing jobs into categories.|[Organize Jobs](../../ssms/agent/organize-jobs.md)|  
|Contains information about the different kinds of job steps you can create and how to manage them.|[Manage Job Steps](../../ssms/agent/manage-job-steps.md)|  
|Contains information about how to define when jobs start running and how often they should run.|[Create and Attach Schedules to Jobs](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Contains information about manually running jobs (without a schedule).|[Run Jobs](../../ssms/agent/run-jobs.md)|  
|Contains information about how you can configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent to respond to jobs. For example, you can configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent to notify administrators when jobs are finished.|[Specify Job Responses](../../ssms/agent/specify-job-responses.md)|  
|Contains information about how to view existing jobs, their history once executes, and how to modify them.|[View or Modify Jobs](../../ssms/agent/view-or-modify-jobs.md)|  
|Contains information about how to delete jobs.|[Delete Jobs](../../ssms/agent/delete-jobs.md)|  
  
## See Also  
[Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)  
