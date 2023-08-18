---
title: "sp_notify_operator (Transact-SQL)"
description: "sp_notify_operator (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "08/09/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_notify_operator_TSQL"
  - "sp_notify_operator"
helpviewer_keywords:
  - "sp_notify_operator"
dev_langs:
  - "TSQL"
---
# sp_notify_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sends an e-mail message to an operator using Database Mail.  
  
 
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## Arguments  
`[ @profile_name = ] 'profilename'`
 The name of the Database Mail profile to use to send the message. *profilename* is **nvarchar(128)**. If *profilename* is not specified, the default Database Mail profile is used.  
  
`[ @id = ] id`
 The identifier for the operator to send the message to. *id* is **int**, with a default of NULL. One of *id* or *name* must be specified.  
  
`[ @name = ] 'name'`
 The name of the operator to send the message to. *name* is **nvarchar(128)**, with a default of NULL. One of *id* or *name* must be specified.  
  
> [!NOTE]  
> An e-mail address must be defined for the operator before they can receive messages.  
  
`[ @subject = ] 'subject'`
 The subject for the e-mail message. *subject* is **nvarchar(256)** with no default.  
  
`[ @body = ] 'message'`
 The body of the e-mail message. *message* is **nvarchar(max)** with no default.  
  
`[ @file_attachments = ] 'attachment'`
 The name of a file to attach to the e-mail message. *attachment* is **nvarchar(512)**, with no default.  
  
`[ @mail_database = ] 'mail_host_database'`
 Specifies the name of the mail host database. *mail_host_database* is **nvarchar(128)**. If no *mail_host_database* is specified, the **msdb** database is used by default.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 Sends the message specified to the e-mail address of the operator specified. If the operator has no e-mail address configured, returns an error.  
  
 Database Mail and a mail host database must be configured before a notification can be sent to an operator.  
  
## Permissions  
 By default, members of the **sysadmin** fixed server role can execute this stored procedure. Other users must be granted one of the following [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent fixed database roles in the **msdb** database:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 For details about the permissions of these roles, see [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## Examples  
 The following example sends a notification e-mail to the operator `François Ajenstat` using the `AdventureWorks Administrator` Database Mail profile. The subject of the e-mail is `Test Notification`. The e-mail message contains the sentence, "This is a test of notification via e-mail."  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## See also  
 [SQL Server Agent Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
