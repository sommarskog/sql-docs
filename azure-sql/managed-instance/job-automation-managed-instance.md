---
title: Job automation with SQL Agent jobs
titleSuffix: Azure SQL Managed Instance
description: "Automation options to run Transact-SQL (T-SQL) scripts in Azure SQL Managed Instance"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: 04/19/2022
ms.service: sql-db-mi
ms.subservice: deployment-configuration
ms.topic: conceptual
ms.custom: sqldbrb=1
dev_langs:
  - TSQL
---
# Automate management tasks using SQL Agent jobs in Azure SQL Managed Instance
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

Using [SQL Server Agent](/sql/ssms/agent/sql-server-agent) in SQL Server and [SQL Managed Instance](sql-managed-instance-paas-overview.md), you can create and schedule jobs that could be periodically executed against one or many databases to run Transact-SQL (T-SQL) queries and perform maintenance tasks. This article covers the use of SQL Agent for SQL Managed Instance.

> [!Note]
> SQL Agent is not available in Azure SQL Database or Azure Synapse Analytics. Instead, we recommend [Job automation with Elastic Jobs](../database/job-automation-overview.md).

## When to use SQL Agent jobs 

There are several scenarios when you could use SQL Agent jobs:

- Automate management tasks and schedule them to run every weekday, after hours, etc.
  - Deploy schema changes, credentials management, performance data collection or tenant (customer) telemetry collection.
  - Update reference data (information common across all databases), load data from Azure Blob storage. Microsoft recommends using [SHARED ACCESS SIGNATURE authentication to authenticate to Azure Blob storage](/sql/t-sql/statements/bulk-insert-transact-sql#f-importing-data-from-a-file-in-azure-blob-storage).
  - Common maintenance tasks including `DBCC CHECKDB` to ensure data integrity or index maintenance to improve query performance. Configure jobs to execute across a collection of databases on a recurring basis, such as during off-peak hours.
  - Collect query results from a set of databases into a central table on an on-going basis. Performance queries can be continually executed and configured to trigger additional tasks to be executed.
- Collect data for reporting
  - Aggregate data from a collection of databases into a single destination table.
  - Execute longer running data processing queries across a large set of databases, for example the collection of customer telemetry. Results are collected into a single destination table for further analysis.
- Data movements
  - Create jobs that replicate changes made in your databases to other databases or collect updates made in remote databases and apply changes in the database.
  - Create jobs that load data from or to your databases using SQL Server Integration Services (SSIS).

## SQL Agent jobs in SQL Managed Instance

SQL Agent Jobs are executed by the SQL Agent service that continues to be used for task automation in SQL Server and SQL Managed Instance. 

SQL Agent Jobs are a specified series of T-SQL scripts against your database. Use jobs to define an administrative task that can be run one or more times and monitored for success or failure. 

A job can run on one local server or on multiple remote servers. SQL Agent Jobs are an internal Database Engine component that is executed within the SQL Managed Instance service.

There are several key concepts in SQL Agent Jobs:

- **Job steps** set of one or many steps that should be executed within the job. For every job step you can define retry strategy and the action that should happen if the job step succeeds or fails.
- **Schedules** define when the job should be executed.
- **Notifications** enable you to define rules that will be used to notify operators via email once the job completes.

## Job steps

SQL Agent Job steps are sequences of actions that SQL Agent should execute. Every step has the following step that should be executed if the step succeeds or fails, number of retries in a case of failure.

SQL Agent enables you to create different types of job steps, such as Transact-SQL job steps that execute a single Transact-SQL batch against the database, or OS command/PowerShell steps that can execute custom OS script, [SSIS job steps](/azure/data-factory/how-to-invoke-ssis-package-managed-instance-agent) that enable you to load data using SSIS runtime, or [replication](../managed-instance/replication-transactional-overview.md) steps that can publish changes from your database to other databases.

> [!Note]
> For more information on leveraging the Azure SSIS Integration Runtime with SSISDB hosted by SQL Managed Instance, see [Use Azure SQL Managed Instance with SQL Server Integration Services (SSIS) in Azure Data Factory](/azure/data-factory/how-to-use-sql-managed-instance-with-ir).

[Transactional replication](../managed-instance/replication-transactional-overview.md) can replicate the changes from your tables into other databases in SQL Managed Instance, Azure SQL Database, or SQL Server. For information, see [Configure replication in Azure SQL Managed Instance](./replication-between-two-instances-configure-tutorial.md). 

Other types of job steps are **not currently supported** in SQL Managed Instance, such as Merge replication, and Queue reader.


 
## Job schedules

A schedule specifies when a job runs. More than one job can run on the same schedule, and more than one schedule can apply to the same job.

A schedule can define the following conditions for the time when a job runs:

- Whenever SQL Server Agent starts. Job is activated after every failover.
- One time, at a specific date and time, which is useful for delayed execution of some job.
- On a recurring schedule.

For more information on scheduling a SQL Agent job, see [Schedule a Job](/sql/ssms/agent/schedule-a-job).

> [!Note]
> Azure SQL Managed Instance currently does not enable you to start a job when the CPU is idle.

## Job notifications

SQL Agent jobs enable you to get notifications when the job finishes successfully or fails. You can receive notifications via email.

If it isn't already enabled, first you would need to configure [the Database Mail feature](/sql/relational-databases/database-mail/database-mail) on SQL Managed Instance:

```sql
GO
EXEC sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
EXEC sp_configure 'Database Mail XPs', 1;
GO
RECONFIGURE
```

As an example exercise, set up the email account that will be used to send the email notifications. Assign the account to the email profile called `AzureManagedInstance_dbmail_profile`. To send e-mail using SQL Agent jobs in SQL Managed Instance, there should be a profile that must be called `AzureManagedInstance_dbmail_profile`. Otherwise, SQL Managed Instance will be unable to send emails via SQL Agent. 

> [!NOTE]
> For the mail server, we recommend you use authenticated SMTP relay services to send email. These relay services typically connect through TCP ports 25 or 587 for connections over TLS, or port 465 for SSL connections, however Database Mail can be configured to use any port. These ports require a new outbound rule in your managed instance's network security group. These services are used to maintain IP and domain reputation to minimize the possibility that external domains reject your messages or put them to the SPAM folder. Consider an authenticated SMTP relay service already in your on-premises servers. In Azure, [SendGrid](https://sendgrid.com/partners/azure/) is one such SMTP relay service, but there are others. 

Use the following sample script to create a Database Mail account and profile, then associate them together:

```sql
-- Create a Database Mail account
EXECUTE msdb.dbo.sysmail_add_account_sp
    @account_name = 'SQL Agent Account',
    @description = 'Mail account for Azure SQL Managed Instance SQL Agent system.',
    @email_address = '$(loginEmail)',
    @display_name = 'SQL Agent Account',
    @mailserver_name = '$(mailserver)' ,
    @username = '$(loginEmail)' ,
    @password = '$(password)';

-- Create a Database Mail profile
EXECUTE msdb.dbo.sysmail_add_profile_sp
    @profile_name = 'AzureManagedInstance_dbmail_profile',
    @description = 'E-mail profile used for messages sent by Managed Instance SQL Agent.';

-- Add the account to the profile
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp
    @profile_name = 'AzureManagedInstance_dbmail_profile',
    @account_name = 'SQL Agent Account',
    @sequence_number = 1;
```

Test the Database Mail configuration via T-SQL using the [sp_send_db_mail](/sql/relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql) system stored procedure:

```sql
DECLARE @body VARCHAR(4000) = 'The email is sent from ' + @@SERVERNAME;
EXEC msdb.dbo.sp_send_dbmail  
    @profile_name = 'AzureManagedInstance_dbmail_profile',  
    @recipients = 'ADD YOUR EMAIL HERE',  
    @body = 'Add some text',  
    @subject = 'Azure SQL Instance - test email';  
```

You can notify the operator that something happened with your SQL Agent jobs. An operator defines contact information for an individual responsible for the maintenance of one or more instances in SQL Managed Instance. Sometimes, operator responsibilities are assigned to one individual.

In systems with multiple instances in SQL Managed Instance or SQL Server, many individuals can share operator responsibilities. An operator does not contain security information, and does not define a security principal. Ideally, an operator is not an individual whose responsibilities may change, but an email distribution group.   

You can [create operators](/sql/relational-databases/system-stored-procedures/sp-add-operator-transact-sql) using SQL Server Management Studio (SSMS) or the Transact-SQL script shown in the following example:

```sql
EXEC msdb.dbo.sp_add_operator
    @name=N'AzureSQLTeam',
    @enabled=1,
    @email_address=N'AzureSQLTeamn@contoso.com';
```

Confirm the email's success or failure via the [Database Mail Log](/sql/relational-databases/database-mail/database-mail-log-and-audits) in SSMS.

You can then [modify any SQL Agent job](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) and assign operators that will be notified via email if the job completes, fails, or succeeds using SSMS or the following T-SQL script:

```sql
EXEC msdb.dbo.sp_update_job @job_name=N'Load data using SSIS',
    @notify_level_email=3, -- Options are: 1 on succeed, 2 on failure, 3 on complete
    @notify_email_operator_name=N'AzureSQLTeam';
```

## Job history

SQL Managed Instance currently doesn't allow you to change any SQL Agent properties because they are stored in the underlying registry values. This means options for adjusting the Agent retention policy for job history records are fixed at the default of 1000 total records and max 100 history records per job.

For more information, see [View SQL Agent job history](/sql/ssms/agent/view-the-job-history).

## Fixed database role membership

If users linked to non-sysadmin logins are added to any of the three SQL Agent fixed database roles in the `msdb` system database, there exists an issue in which explicit EXECUTE permissions need to be granted to three system stored procedures in the `master` database. If this issue is encountered, the error message `The EXECUTE permission was denied on the object <object_name> (Microsoft SQL Server, Error: 229)` will be shown. 

Once you add users to a SQL Agent fixed database role (SQLAgentUserRole, SQLAgentReaderRole, or SQLAgentOperatorRole) in `msdb`, for each of the user's logins added to these roles, execute the below T-SQL script to explicitly grant EXECUTE permissions to the system stored procedures listed. This example assumes that the user name and login name are the same:

```sql
USE [master]
GO
CREATE USER [login_name] FOR LOGIN [login_name];
GO
GRANT EXECUTE ON master.dbo.xp_sqlagent_enum_jobs TO [login_name];
GRANT EXECUTE ON master.dbo.xp_sqlagent_is_starting TO [login_name];
GRANT EXECUTE ON master.dbo.xp_sqlagent_notify TO [login_name];
```

## SQL Agent job limitations in SQL Managed Instance

It is worth noting the differences between SQL Agent available in SQL Server and as part of SQL Managed Instance. For more on the supported feature differences between SQL Server and SQL Managed Instance, see [Azure SQL Managed Instance T-SQL differences from SQL Server](./transact-sql-tsql-differences-sql-server.md#sql-server-agent). 

Some of the SQL Agent features that are available in SQL Server are not supported in SQL Managed Instance:

- SQL Agent settings are read only. 
    - The system stored procedure `sp_set_agent_properties` is not supported.
- Enabling/disabling SQL Agent is currently not supported. SQL Agent is always running.
- While notifications are partially supported, the following are not supported:
  - Pager is not supported.
  - NetSend is not supported.
  - Alerts are not supported.
- Proxies are not supported.
- Eventlog is not supported.
- Job schedule trigger based on an idle CPU is not supported.
- Merge replication job steps are not supported.
- Queue Reader is not supported. 
- Analysis Services is not supported. 
- Running a script stored as a file on disk is not supported. 
- Importing external modules, such as dbatools and dbachecks, are not supported. 
- PowerShell Core is not supported. 

## Learn more

- [What is Azure SQL Managed Instance?](../managed-instance/sql-managed-instance-paas-overview.md)
- [What's new in Azure SQL Managed Instance?](doc-changes-updates-release-notes-whats-new.md)
- [Azure SQL Managed Instance T-SQL differences from SQL Server](./transact-sql-tsql-differences-sql-server.md#sql-server-agent)
- [Features comparison: Azure SQL Database and Azure SQL Managed Instance](../database/features-comparison.md)


## Next steps

- [Configure Database Mail](/sql/relational-databases/database-mail/configure-database-mail)
- [Troubleshoot outbound SMTP connectivity problems in Azure](/azure/virtual-network/troubleshoot-outbound-smtp-connectivity)
