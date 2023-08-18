---
title: "ALTER SERVER CONFIGURATION (Transact-SQL)"
description: ALTER SERVER CONFIGURATION (Transact-SQL)
author: markingmyname
ms.author: maghan
ms.date: 05/22/2019
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ALTER SERVER CONFIGURATION"
  - "ALTER_SERVER_CONFIGURATION_TSQL"
helpviewer_keywords:
  - "SERVER CONFIGURATION, ALTER"
  - "process affinity, setting"
  - "ALTER SERVER CONFIGURATION statement"
  - "setting process affinity"
dev_langs:
  - "TSQL"
---
# ALTER SERVER CONFIGURATION (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Modifies global configuration settings for the current server in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  

```syntaxsql
ALTER SERVER CONFIGURATION  
SET <optionspec>   
[;]  
  
<optionspec> ::=  
{  
     <process_affinity>  
   | <diagnostic_log>  
   | <failover_cluster_property>  
   | <hadr_cluster_context>  
   | <buffer_pool_extension>  
   | <soft_numa>  
   | <memory_optimized>
   | <hardware_offload>
   | <suspend_for_snapshot_backup>
}  
  
<process_affinity> ::=   
   PROCESS AFFINITY   
   {  
     CPU = { AUTO | <CPU_range_spec> }   
   | NUMANODE = <NUMA_node_range_spec>   
   }  
   <CPU_range_spec> ::=   
      { CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]   
  
   <NUMA_node_range_spec> ::=   
      { NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID } [ ,...n ]  
  
<diagnostic_log> ::=   
   DIAGNOSTICS LOG   
   {   
     ON    
   | OFF    
   | PATH = { 'os_file_path' | DEFAULT }    
   | MAX_SIZE = { 'log_max_size' MB | DEFAULT }    
   | MAX_FILES = { 'max_file_count' | DEFAULT }    
   }  
  
<failover_cluster_property> ::=   
   FAILOVER CLUSTER PROPERTY <resource_property>  
   <resource_property> ::=  
      {  
        VerboseLogging = { 'logging_detail' | DEFAULT }    
      | SqlDumperDumpFlags = { 'dump_file_type' | DEFAULT }  
      | SqlDumperDumpPath = { 'os_file_path'| DEFAULT }  
      | SqlDumperDumpTimeOut = { 'dump_time-out' | DEFAULT }  
      | FailureConditionLevel = { 'failure_condition_level' | DEFAULT }  
      | HealthCheckTimeout = { 'health_check_time-out' | DEFAULT }  
      }  
  
<hadr_cluster_context> ::=  
   HADR CLUSTER CONTEXT = { 'remote_windows_cluster' | LOCAL }  
  
<buffer_pool_extension>::=  
    BUFFER POOL EXTENSION   
    { ON ( FILENAME = 'os_file_path_and_name' , SIZE = <size_spec> )   
    | OFF }  
  
    <size_spec> ::=  
        { size [ KB | MB | GB ] }  
  
<soft_numa> ::=  
    SOFTNUMA  
    { ON | OFF }  

<memory-optimized> ::=   
   MEMORY_OPTIMIZED   
   {   
     ON 
   | OFF
   | [ TEMPDB_METADATA = { ON [(RESOURCE_POOL='resource_pool_name')] | OFF }
   | [ HYBRID_BUFFER_POOL = { ON | OFF }
   }  

<hardware_offload> ::=
   HARDWARE_OFFLOAD
   {   
     ON 
   | OFF
   }

<suspend_for_snapshot_backup> ::=
    SET SUSPEND_FOR_SNAPSHOT_BACKUP = { ON | OFF } [ ( GROUP = ( <database>,...n) [ , MODE = COPY_ONLY ] ) ]

```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
**\<process_affinity> ::=**  
  
PROCESS AFFINITY  
Enables hardware threads to be associated with CPUs.  
  
CPU = { AUTO | \<CPU_range_spec> }  
Distributes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] worker threads to each CPU within the specified range. CPUs outside the specified range won't have assigned threads.  
  
AUTO  
Specifies that no thread is assigned a CPU. The operating system can freely move threads among CPUs based on the server workload. This setting is the default and is recommended.  
  
\<CPU_range_spec> ::=  
Specifies the CPU or range of CPUs to assign threads to.  
  
{ CPU_ID | CPU_ID  TO  CPU_ID } [ ,...n ]  
Is the list of one or more CPUs. CPU IDs begin at 0 and are **integer** values.  
  
NUMANODE = \<NUMA_node_range_spec>  
Assigns threads to all CPUs that belong to the specified NUMA node or range of nodes.  
  
\<NUMA_node_range_spec> ::=  
Specifies the NUMA node or range of NUMA nodes.  
  
{ NUMA_node_ID | NUMA_node_ID  TO NUMA_node_ID } [ ,...n ]  
Is the list of one or more NUMA nodes. NUMA node IDs begin at 0 and are **integer** values.  
  
**\<diagnostic_log> ::=**  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).  

  
DIAGNOSTICS LOG  
Starts or stops logging diagnostic data that the sp_server_diagnostics procedure captures. This argument also sets SQLDIAG log configuration parameters such as the log file rollover count, log file size, and file location. For more information, see [View and Read Failover Cluster Instance Diagnostics Log](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md).  
  
ON  
Starts [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logging diagnostic data in the location specified in the PATH file option. This argument is the default.  
  
OFF  
Stops logging diagnostic data.  
  
PATH = { 'os_file_path' | DEFAULT }  
Path indicating the location of the diagnostic logs. The default location is \<\MSSQL\Log> within the installation folder of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster instance.  
  
MAX_SIZE = { 'log_max_size' MB | DEFAULT }  
Maximum size in megabytes to which each diagnostic log can grow. The default is 100 MB.  
  
MAX_FILES = { 'max_file_count' | DEFAULT }  
Maximum number of diagnostic log files that can be stored on the computer before they're recycled for new diagnostic logs.  
  
**\<failover_cluster_property> ::=**  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).    
  
FAILOVER CLUSTER PROPERTY  
Modifies the SQL Server resource private failover cluster properties.  
  
VERBOSE LOGGING = { 'logging_detail' | DEFAULT }  
Sets the logging level for SQL Server Failover Clustering. It can be turned on to provide additional details in the error logs for troubleshooting.  
  
-   0 - Logging is turned off (default)  
  
-   1 - Errors only  
  
-   2 - Errors and warnings  
  
In resource failover scenarios, the SQL Server resource DLL can obtain a dump file before a failover occurs. This applies to both FCI and Availability Group technologies. When the SQL Server resource DLL determines that a SQL Server resource has failed, the SQL Server resource DLL uses the Sqldumper.exe utility to obtain a dump file of the SQL Server process. To make sure that the Sqldumper.exe utility successfully generates the dump file upon resource failover, you must set the following three properties as prerequisites: SqlDumperDumpTimeOut, SqlDumperDumpPath, SqlDumperDumpFlags.

SQLDUMPEREDUMPFLAGS  
Determines the type of dump files generated by SQL Server SQLDumper utility. The default setting is 0. Decimal, instead of hexadecimal, values are used for this setting. For mini dump use 288, for mini dump with indirect memory use 296, for filtered dump use 33024. For more information, see [SQL Server Dumper Utility Knowledgebase article](/troubleshoot/sql/tools/use-sqldumper-generate-dump-file).  
  
SQLDUMPERDUMPPATH = { 'os_file_path' | DEFAULT }  
The location where the SQLDumper utility stores the dump files. For more information, see [SQL Server Dumper Utility Knowledgebase article](/troubleshoot/sql/tools/use-sqldumper-generate-dump-file).  
  
SQLDUMPERDUMPTIMEOUT = { 'dump_time-out' | DEFAULT }  
The time-out value in milliseconds for the SQLDumper utility to generate a dump if a SQL Server failure occurs. The default value is 0, which means there's no time limit to complete the dump. For more information, see [SQL Server Dumper Utility Knowledgebase article](/troubleshoot/sql/tools/use-sqldumper-generate-dump-file).  
  
 FAILURECONDITIONLEVEL = { 'failure_condition_level' | DEFAULT }  
 The conditions under which the SQL Server failover cluster instance should fail over  or restart. The default value is 3, which means that the SQL Server resource will fail over or restart on critical server errors. For more information about this and other failure condition levels, see [Configure FailureConditionLevel Property Settings](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).  
  
HEALTHCHECKTIMEOUT = { 'health_check_time-out' | DEFAULT }  
The time-out value for how long the SQL Server Database Engine resource DLL should wait for the server health information before it considers the instance of SQL Server as unresponsive. The time-out value is expressed in milliseconds. The default is 60,000 milliseconds (60 seconds).  
  
**\<hadr_cluster_context> ::=**  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).   
  
HADR CLUSTER CONTEXT **=** { **'**_remote\_windows\_cluster_**'** | LOCAL }  
Switches the HADR cluster context of the server instance to the specified Windows Server Failover Cluster (WSFC). The *HADR cluster context* determines what WSFC manages the metadata for availability replicas hosted by the server instance. Use the SET HADR CLUSTER CONTEXT option only during a cross-cluster migration of [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] to an instance of [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] or higher version on a new WSFC r.  
  
You can switch the HADR cluster context only from the local WSFC to a remote WSFC. Then, you may choose to switch back from the remote WSFC to the local WSFC. The HADR cluster context can be switched to a remote cluster only when the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] isn't hosting any availability replicas.  
  
A remote HADR cluster context can be switched back to the local cluster at any time. However, the context can't be switched again as long as the server instance is hosting any availability replicas. 
  
To identify the destination cluster, specify one of the following values:  
  
*windows_cluster*  
The network name of a WSFC. You can specify either the short name or the full domain name. To find the target IP address of a short name, ALTER SERVER CONFIGURATION uses DNS resolution. In some circumstances, a short name could cause confusion, and DNS could return the wrong IP address. We recommend that you specify the full domain name.  
  
> [!NOTE] 
> A cross-cluster migration using this setting is no longer supported. To perform a cross-cluster migration, use a Distributed Availability Group or some other method such as log shipping. 
  
LOCAL  
The local WSFC.  
  
For more information, see [Change the HADR Cluster Context of Server Instance &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md).  
  
**\<buffer_pool_extension>::=**  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]).    
  
ON  
Enables the buffer pool extension option. This option extends the size of the buffer pool by using nonvolatile storage. Nonvolatile storage such as solid-state drives (SSD) persist clean data pages in the pool. For more information about this feature, see [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md).The buffer pool extension isn't available in every SQL Server edition. For more information, see [Editions and supported features of SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md).  
  
FILENAME = 'os_file_path_and_name'  
Defines the directory path and name of the buffer pool extension cache file. The file extension must be specified as .BPE. Turn off BUFFER POOL EXTENSION before you modify FILENAME.  
  
SIZE = *size* [ **KB** | MB | GB ]  
Defines the size of the cache. The default size specification is KB. The minimum size is the size of Max Server Memory. The maximum limit is 32 times the size of Max Server Memory. For more information about Max Server Memory, see [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
Turn off BUFFER POOL EXTENSION before you modify the size of the file. To specify a size that is smaller than the current size, the instance of SQL Server must be restarted to reclaim memory. Otherwise, the specified size must be the same as or larger than the current size.  
  
OFF  
Disables the buffer pool extension option. Disable the buffer pool extension option before you modify any associated parameters such as the size or name of the file. When this option is disabled, all related configuration information is removed from the registry.  
  
> [!WARNING]  
>  Disabling the buffer pool extension might have a negative impact server performance because the buffer pool is significantly reduced in size.  
  
**\<soft_numa>**  

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]).  
  
ON  
Enables automatic partitioning to split large NUMA hardware nodes into smaller NUMA nodes. Changing the running value requires a restart of the database engine.  
  
OFF  
Disables automatic software partitioning of large NUMA hardware nodes into smaller NUMA nodes. Changing the running value requires a restart of the database engine.  

> [!WARNING]
> There are known issues with the behavior of the ALTER SERVER CONFIGURATION statement with the SOFT NUMA option and SQL Server Agent.  The following is the recommended sequence of operations:  
> 1) Stop the instance of SQL Server Agent.  
> 2) Execute your ALTER SERVER CONFIGURATION  SOFT NUMA option.  
> 3) Re-start the SQL Server instance.  
> 4) Start the instance of SQL Server Agent.  
  
**More Information:** If you run the ALTER SERVER CONFIGURATION with SET SOFTNUMA command before the SQL Server service restarts, then when the SQL Server Agent service stops, it runs a T-SQL RECONFIGURE command that reverts the SOFTNUMA settings back to what they were before the ALTER SERVER CONFIGURATION. 

**\<memory_optimized> ::=**

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)]).

ON <br>
Enables all instance-level features that are part of the [In-Memory Database](../../relational-databases/in-memory-database.md) feature family. This currently includes [memory-optimized tempdb metadata](../../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata) and [hybrid buffer pool](../../database-engine/configure-windows/hybrid-buffer-pool.md). Requires a restart to take effect.

OFF <br>
Disables all instance-level features that are part of the In-Memory Database feature family. Requires a restart to take effect.

TEMPDB_METADATA = ON | OFF <br>
Enables or disables memory-optimized tempdb metadata only. Requires a restart to take effect. 

RESOURCE_POOL='resource_pool_name' <br>
When combined with TEMPDB_METADATA = ON, specifies the user-defined resource pool that should be used for tempdb. If not specified, tempdb will use the default pool. The pool must already exist. If the pool is not available when the service is restarted, tempdb will use the default pool.


HYBRID_BUFFER_POOL = ON | OFF <br>
Enables or disables hybrid buffer pool at the instance level. Requires a restart to take effect.

**\<hardware_offload> ::=**

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[sql-server-2022](../../includes/sssql22-md.md)]).

ON <br>
Enables the use of integrated acceleration and offloading for the instance.  Requires restart.

OFF <br>
Disables all instance-level use of integrated acceleration and offloading. Requires a restart to take effect.

For more information, see [Integrated acceleration and offloading](../../relational-databases/integrated-acceleration/overview.md).

**\<suspend_for_snapshot_backup> ::=**

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL22](../../includes/sssql22-md.md)])

Suspends databases for snapshot backup. May define a group of one or more databases. May designate copy only mode.

SET SUSPEND_FOR_SNAPSHOT_BACKUP = { ON | **OFF** }

Suspends, or un-suspends databases. Default OFF.

GROUP = ( \<database>,...n)

Optional. Defines a group of one or more databases to suspend. If not specified, the setting applies to all databases.

MODE = COPY_ONLY

Optional. Uses COPY_ONLY mode for all database backups.

## General Remarks  
This statement doesn't require a restart of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], unless explicitly stated otherwise. If it's a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster instance, it doesn't require a restart of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cluster resource.  
  
## Limitations and Restrictions  
This statement doesn't support DDL triggers.  
  
## Permissions  
Requires:
- `ALTER SETTINGS` permissions for the process affinity option.
- `ALTER SETTINGS` and `VIEW SERVER STATE` permissions for the diagnostic log and failover cluster property options.
- `CONTROL SERVER` permission for the HADR cluster context option.  
- `ALTER SERVER STATE` permission for the buffer pool extension option.  
  
The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] resource DLL runs under the Local System account. As such, the Local System account must have read and write access to the specified path in the Diagnostic Log option.  
  
## Examples  
  
|Category|Featured syntax elements|  
|--------------|------------------------------|  
|[Setting process affinity](#Affinity)|CPU • NUMANODE • AUTO|  
|[Setting diagnostic log options](#Diagnostic)|ON • OFF • PATH • MAX_SIZE|  
|[Setting failover cluster properties](#Failover)|HealthCheckTimeout|  
|[Changing the cluster context of an availability replica](#ChangeClusterContextExample)|**'** *windows_cluster* **'**|  
|[Setting the buffer pool extension](#BufferPoolExtension)|BUFFER POOL EXTENSION| 
|[Setting In-Memory Database options](#MemoryOptimized)|MEMORY_OPTIMIZED|

  
###  <a name="Affinity"></a> Setting process affinity  
The examples in this section show how to set process affinity to CPUs and NUMA nodes. The examples assume that the server contains 256 CPUs that are arranged into four groups of 16 NUMA nodes each. Threads aren't assigned to any NUMA node or CPU.  
  
-   Group 0: NUMA nodes 0 through 3, CPUs 0 to 63  
-   Group 1: NUMA nodes 4 through 7, CPUs 64 to 127  
-   Group 2: NUMA nodes 8 through 12, CPUs 128 to 191  
-   Group 3: NUMA nodes 13 through 16, CPUs 192 to 255  
  
#### A. Setting affinity to all CPUs in groups 0 and 2  
The following example sets affinity to all the CPUs in groups 0 and 2.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 63, 128 TO 191;  
```  
  
#### B. Setting affinity to all CPUs in NUMA nodes 0 and 7  
The following example sets the CPU affinity to nodes `0` and `7` only.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY NUMANODE=0, 7;  
```  
  
#### C. Setting affinity to CPUs 60 through 200  
The following example sets affinity to CPUs 60 through 200.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=60 TO 200;  
```  
  
#### D. Setting affinity to CPU 0 on a system that has two CPUs  
The following example sets the affinity to `CPU=0` on a computer that has two CPUs. Before the following statement is executed, the internal affinity bitmask is 00.  
  
```sql  
ALTER SERVER CONFIGURATION SET PROCESS AFFINITY CPU=0;  
```  
  
#### E. Setting affinity to AUTO  
The following example sets affinity to `AUTO`.  
  
```sql  
ALTER SERVER CONFIGURATION  
SET PROCESS AFFINITY CPU=AUTO;  
```  
  
###  <a name="Diagnostic"></a> Setting diagnostic log options  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).    
  
The examples in this section show how to set the values for the diagnostic log option.  
  
#### A. Starting diagnostic logging  
The following example starts the logging of diagnostic data.  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
#### B. Stopping diagnostic logging  
The following example stops the logging of diagnostic data.  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
#### C. Specifying the location of the diagnostic logs  
The following example sets the location of the diagnostic logs to the specified file path.  
  
```sql  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
#### D. Specifying the maximum size of each diagnostic log  
The following example set the maximum size of each diagnostic log to 10 megabytes.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
###  <a name="Failover"></a> Setting failover cluster properties  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]).   
  
The following example illustrates setting the values of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster resource properties.  
  
#### A. Specifying the value for the HealthCheckTimeout property  
The following example sets the `HealthCheckTimeout` option to 15,000 milliseconds (15 seconds).  
  
```sql  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
###  <a name="ChangeClusterContextExample"></a> B. Changing the cluster context of an availability replica  
The following example changes the HADR cluster context of the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. To specify the destination WSFC cluster, `clus01`, the example specifies the full cluster object name, `clus01.xyz.com`.  
  
```sql  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
### Setting Buffer Pool Extension Options  
  
####  <a name="BufferPoolExtension"></a> A. Setting the buffer pool extension option  
  
**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]).    
  
The following example enables the buffer pool extension option and specifies a file name and size.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 50 GB);  
```  
  
#### B. Modifying buffer pool extension parameters  
The following example modifies the size of a buffer pool extension file. The buffer pool extension option must be disabled before any of the parameters are modified.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION OFF;  
GO  
EXEC sp_configure 'max server memory (MB)', 12000;  
GO  
RECONFIGURE;  
GO  
ALTER SERVER CONFIGURATION  
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 60 GB);  
GO   
```  

### <a name="MemoryOptimized"></a> Setting In-Memory Database Options

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (starting with [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)]).

#### A. Enable all In-Memory Database features with default options

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED ON;
GO
```

#### B. Enable memory-optimized tempdb metadata using the default resource pool

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
GO
```

#### C. Enable memory-optimized tempdb metadata with a user-defined resource pool

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
GO
```

#### D. Enable hybrid buffer pool

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
GO
```

## See Also  
[Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)   
[Change the HADR Cluster Context of Server Instance &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)   
[sys.dm_os_schedulers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)   
[sys.dm_os_memory_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)   
[sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)   
[Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md)  
