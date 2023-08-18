---
title: "catalog.execution_data_taps"
description: "catalog.execution_data_taps"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.execution_data_taps 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  Displays information for each data tap defined in an execution.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|Unique identifier (ID) of the data tap.|  
|execution_id|**bigint**|Unique identifier (ID) for the instance of execution.|  
|package_path|**nvarchar(max)**|The package path for the data flow task where the data is tapped.|  
|dataflow_path_id_string|**nvarchar(4000)**|The identification string of the data flow path.|  
|dataflow_task_guid|**uniqueidentifier**|Unique ID of the data flow task.|  
|max_rows|**int**|The number of rows to be captured. If this value is not specified then all rows will be captured.|  
|filename|**nvarchar(4000)**|The name of the data dump file. For more information, see [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## Permissions  
 This view requires one of the following permissions:  
  
-   READ permission on the instance of execution  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
> [!NOTE]  
>  When you have permission to perform an operation on the server, you also have permission to view information about the operation. Row-level security is enforced; only rows that you have permission to view are displayed.  
  
## See Also  
 [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
