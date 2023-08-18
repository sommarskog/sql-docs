---
title: "CREATE RESOURCE POOL (Transact-SQL)"
description: CREATE RESOURCE POOL (Transact-SQL)
author: markingmyname
ms.author: maghan
ms.date: "08/10/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "CREATE RESOURCE POOL"
  - "RESOURCE POOL"
  - "CREATE_RESOURCE_POOL_TSQL"
  - "RESOURCE_POOL_TSQL"
helpviewer_keywords:
  - "CREATE RESOURCE POOL"
dev_langs:
  - "TSQL"
---
# CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sql-asdbmi.md)]

Creates a Resource Governor resource pool in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A resource pool represents a subset of the physical resources (memory, CPUs and IO) of an instance of the Database Engine. Resource Governor enables a database administrator to distribute server resources among resource pools, up to a maximum of 64 pools. Resource Governor is not available in every edition of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of features that are supported by the editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see [Features Supported by the Editions of SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
```syntaxsql
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,...n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,...n]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
*pool_name*  
Is the user-defined name for the resource pool. *pool_name* is alphanumeric, can be up to 128 characters, must be unique within an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], and must comply with the rules for [identifiers](../../relational-databases/databases/database-identifiers.md).  
  
MIN_CPU_PERCENT =*value*  
Specifies the guaranteed average CPU bandwidth for all requests in the resource pool when there is CPU contention. *value* is an integer with a default setting of 0. The allowed range for *value* is from 0 through 100.  
  
MAX_CPU_PERCENT =*value*  
Specifies the maximum average CPU bandwidth that all requests in resource pool will receive when there is CPU contention. *value* is an integer with a default setting of 100. The allowed range for *value* is from 1 through 100.  
  
CAP_CPU_PERCENT =*value*   
**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.  
  
Specifies a hard cap on the CPU bandwidth that all requests in the resource pool will receive. Limits the maximum CPU bandwidth level to be the same as the specified value. *value* is an integer with a default setting of 100. The allowed range for *value* is from 1 through 100.  
  
AFFINITY {SCHEDULER = AUTO | ( \<scheduler_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)}      
**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.  
  
Attach the resource pool to specific schedulers. The default value is AUTO.  
  
AFFINITY SCHEDULER = **(** \<scheduler_range_spec> **)** maps the resource pool to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schedules identified by the given IDs. These IDs map to the values in the scheduler_id column in [sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 
  
When you use AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)**, the resource pool is affinitized to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schedulers that map to the physical CPUs that correspond to the given NUMA node or range of nodes. You can use the following [!INCLUDE[tsql](../../includes/tsql-md.md)] query to discover the mapping between the physical NUMA configuration and the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] scheduler IDs. 
  
```sql  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
MIN_MEMORY_PERCENT =*value*    
Specifies the minimum amount of memory reserved for this resource pool that can not be shared with other resource pools. *value* is an integer with a default setting of 0 The allowed range for *value* is from 0 to 100.  
  
MAX_MEMORY_PERCENT =*value*    
Specifies the total server memory that can be used by requests in this resource pool. *value* is an integer with a default setting of 100. The allowed range for *value* is from 1 through 100.  
  
MIN_IOPS_PER_VOLUME =*value*    
**Applies to**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] and later.  
  
Specifies the minimum I/O operations per second (IOPS) per disk volume to reserve for the resource pool. The allowed range for *value* is from 0 through 2^31-1 (2,147,483,647). Specify 0 to indicate no minimum threshold for the pool. The default is 0.  
  
MAX_IOPS_PER_VOLUME =*value*    
**Applies to**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] and later.  
  
Specifies the maximum I/O operations per second (IOPS) per disk volume to allow for the resource pool. The allowed range for *value* is from 0 through 2^31-1 (2,147,483,647). Specify 0 to set an unlimited threshold for the pool. The default is 0.  
  
If the `MAX_IOPS_PER_VOLUME` for a pool is set to 0, the pool is not governed at all and can take all the IOPS in the system even if other pools have MIN_IOPS_PER_VOLUME set. For this case, we recommend that you set the `MAX_IOPS_PER_VOLUME` value for this pool to a high number (for example, the maximum value 2^31-1) if you want this pool to be governed for IO.  
  
## Remarks  
`MIN_IOPS_PER_VOLUME` and `MAX_IOPS_PER_VOLUME` specify the minimum and maximum reads or writes per second. These reads or writes can be of any size and do not indicate minimum or maximum throughput.  
  
The values for `MAX_CPU_PERCENT` and `MAX_MEMORY_PERCENT` must be greater than or equal to the values for `MIN_CPU_PERCENT` and `MIN_MEMORY_PERCENT`, respectively.  
  
`CAP_CPU_PERCENT` differs from `MAX_CPU_PERCENT` in that workloads associated with the pool can use CPU capacity above the value of `MAX_CPU_PERCENT` if it is available, but not above the value of `CAP_CPU_PERCENT`.  
  
The total CPU percentage for each affinitized component (scheduler(s) or NUMA node(s)) should not exceed 100 percent.  
  
## Permissions  
Requires `CONTROL SERVER` permission.  
  
## Examples  
### 1. Shows how to create a resource pool

This example created a resource pool named "bigPool". This pool uses the default Resource Governor settings.  
  
```sql  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### 2. Set the CAP_CPU_PERCENT to a hard cap and set AFFINITY SCHEDULER

Set the CAP_CPU_PERCENT to a hard cap of 30 percent and sets AFFINITY SCHEDULER to a range of 0 to 63, 128 to 191. 
  
**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
```  
  
### 3. Set MIN_IOPS_PER_VOLUME and MAX_IOPS_PER_VOLUME   

Set MIN_IOPS_PER_VOLUME to 20 and MAX_IOPS_PER_VOLUME to 100. These values govern the physical I/O read and write operations that are available for the resource pool.  
  
**Applies to**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] and later.  
  
```sql  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
```  
  
## See Also  
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)     
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)     
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)     
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)     
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)     
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)     
 [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)     
 [Create a Resource Pool](../../relational-databases/resource-governor/create-a-resource-pool.md)    
  
