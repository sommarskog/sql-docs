---
title: "dm_execution_performance_counters (SSISDB Database)"
description: "dm_execution_performance_counters (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# Functions - dm_execution_performance_counters

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

  Returns the performance statistics for an execution that is running on the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] server.  
  
## Syntax  
  
```sql  
dm_execution_performance_counters [ @execution_id = ] execution_id  
  
```  
  
## Arguments  
 [ @execution_id = ] *execution_id*  
 The unique identifier of the execution that contains one or more packages. Packages that are executed with the Execute Package task, run in the same execution as the parent package.  
  
 If an execution ID is not specified, performance statistics for multiple executions are returned. If you are a member of the **ssis_admin** database role, performance statistics for all running executions are returned.  If you are not a member of the **ssis_admin** database role, performance statistics for the running executions for which you have read permissions, are returned. The *execution_id* is a **BigInt**.  
  
## Remarks  
 The following table lists the counter name values returned by the dm_execution_performance_counter function.  
  
|Counter Name|Description|  
|------------------|-----------------|  
|BLOB bytes read|Number of bytes of binary large object (BLOB) data that the data flow engine reads from all sources.|  
|BLOB bytes written|Number of bytes of BLOB data that the data flow engine writes to all destinations.|  
|BLOB files in use|Number of BLOB files that the data flow engine is using for spooling.|  
|Buffer memory|Amount of memory that is used by the Integration Services buffers, including physical and virtual memory.|  
|Buffers in use|Number of buffer objects, of all types, that all data flow components and the data flow engine are using.|  
|Buffers spooled|Number of buffers written to the disk.|  
|Flat buffer memory|Amount of memory, in bytes, that is used by all flat buffers. Flat buffers are blocks of memory that a component uses to store data.|  
|Flat buffers in use|Number of flat buffers that the data flow engine uses. All flat buffers are private buffers.|  
|Private buffer memory|Amount of memory in use by all private buffers. A private buffer is a buffer that a transformation uses for temporary work.<br /><br /> A buffer is not private if the data flow engine creates the buffer to support the data flow.|  
|Private buffers in use|Number of buffers that the transformations use for temporary work.|  
|Rows read|Total number of rows read by the execution.|  
|Rows written|Total number of rows written by the execution.|  
  
## Return  
 The dm_execution_performance_counters function returns a table with the following columns, for a running execution. The information returned is for all of the packages contained in the execution. If there are no running executions, an empty table is returned.  
  
|Column Name|Column Type|Description|Remarks|  
|-----------------|-----------------|-----------------|-------------|  
|execution_id|**BigInt**<br /><br /> **NULL** is not a valid value.|Unique identifier for the execution that contains the package.||  
|counter_name|**nvarchar(128)**|The name of the counter.|See the **Remarks** section of values.|  
|counter_value|**BigInt**|Value returned by the counter.||  
  
## Examples  

### A. Return statistics for a running execution

 In the following example, the function returns statistics for a running execution with an ID of 34.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (34)  
```  
  
### B. Return statistics for all running executions

 In the following example, the function returns statistics for all the executions running on the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] server, depending on your permissions.  
  
```sql
select * from [catalog].[dm_execution_performance_counters] (NULL)  
  
```  
  
## Permissions  
 This function requires one of the following permissions:  
  
-   READ and MODIFY permissions on the instance of execution  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes conditions that cause the function to fail.  
  
-   The user does not have MODIFY permissions for the specified execution.  
  
-   The specified execution ID is not valid.  
  
  
