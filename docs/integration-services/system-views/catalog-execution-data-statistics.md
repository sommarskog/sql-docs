---
title: "catalog.execution_data_statistics"
description: "catalog.execution_data_statistics"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.execution_data_statistics 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  This view displays a row each time a data flow component sends data to a downstream component, for a given package execution. The information in this view can be used to compute the data throughput for a component.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|Unique identifier (ID) of the data.|  
|execution_id|**bigint**|Unique ID for the instance of execution.|  
|package_name|**nvarchar(260)**|The name of the first package that was started during execution.|  
|task_name|**nvarchar(4000)**|The name of the data flow task.|  
|dataflow_path_id_string|**nvarchar(4000)**|The identification string of the data flow path.|  
|dataflow_path_name|**nvarchar(4000)**|The name of the data flow path.|  
|source_component_name|**nvarchar(4000)**|The name of the data flow component that sent the data.|  
|destination_component_name|**nvarchar(4000)**|The name of the data flow component that received the data.|  
|rows_sent|**bigint**|The number of rows sent from the source component.|  
|created_time|**datatimeoffset(7)**|The time when the values were obtained.|  
|execution_path|**nvarchar(max)**|The execution path of the component.|  
  
## Remarks  
  
-   When there are multiple outputs from the component, a row is added for each of the outputs.  
  
-   By default, when an execution is started, the information about the number of rows that are sent is not logged.  
  
-   To view this data for a given package execution, set the logging level to **Verbose**. For more information, see [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## Permissions  
 This view requires one of the following permissions:  
  
-   READ permission on the instance of execution  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
> [!NOTE]  
>  When you have permission to perform an operation on the server, you also have permission to view information about the operation. Row-level security is enforced; only rows that you have permission to view are displayed.  
  
  
