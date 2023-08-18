---
title: "sp_start_job (Transact-SQL)"
description: "sp_start_job (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_start_job"
  - "sp_start_job_TSQL"
helpviewer_keywords:
  - "sp_start_job"
dev_langs:
  - "TSQL"
---
# sp_start_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Instructs [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent to execute a job immediately.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_start_job   
     {   [@job_name =] 'job_name'  
       | [@job_id =] job_id }  
     [ , [@error_flag =] error_flag]  
     [ , [@server_name =] 'server_name']  
     [ , [@step_name =] 'step_name']  
     [ , [@output_flag =] output_flag]  
```  
  
## Arguments  
`[ @job_name = ] 'job_name'`
 The name of the job to start. Either *job_id* or *job_name* must be specified, but both cannot be specified. *job_name* is **sysname**, with a default of NULL.  
  
`[ @job_id = ] job_id`
 The identification number of the job to start. Either *job_id* or *job_name* must be specified, but both cannot be specified. *job_id* is **uniqueidentifier**, with a default of NULL.  
  
`[ @error_flag = ] error_flag`
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @server_name = ] 'server_name'`
 The target server on which to start the job. *server_name* is **nvarchar(128)**, with a default of NULL. *server_name* must be one of the target servers to which the job is currently targeted.  
  
`[ @step_name = ] 'step_name'`
 The name of the step at which to begin execution of the job. Applies only to local jobs. *step_name* is **sysname**, with a default of NULL  
  
`[ @output_flag = ] output_flag`
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 This stored procedure is in the **msdb** database.  
  
## Permissions  
 By default, members of the **sysadmin** fixed server role can execute this stored procedure. Other users must be granted one of the following [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent fixed database roles in the **msdb** database:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 For details about the permissions of these roles, see [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
 Members of **SQLAgentUserRole** and **SQLAgentReaderRole** can only start jobs that they own. Members of **SQLAgentOperatorRole** can start all local jobs including those that are owned by other users. Members of **sysadmin** can start all local and multiserver jobs.  
  
## Examples  
 The following example starts a job named `Weekly Sales Data Backup`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
GO  
```  
  
## See Also  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
