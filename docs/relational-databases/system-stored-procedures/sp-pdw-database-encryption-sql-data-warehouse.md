---
title: "sp_pdw_database_encryption (Azure Synapse Analytics)"
description: "sp_pdw_database_encryption (Azure Synapse Analytics)"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/03/2017"
ms.service: sql
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azure-sqldw-latest"
---
# sp_pdw_database_encryption (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use **sp_pdw_database_encryption** to enable transparent data encryption on for a [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] appliance. When **sp_pdw_database_encryption** set to 1, use the **ALTER DATABASE** statement to encrypt a database by using TDE.  
  
## Syntax  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

#### Parameters  
`[ @enabled = ] enabled`
 Determines whether transparent data encryption is enabled. *enabled* is **int**, and can be one of the following values:  
  
-   0 = Disabled  
  
-   1 = Enabled  
  
 Executing **sp_pdw_database_encryption** without parameters returns the current state of TDE on the appliance as a scalar result set: 0 for disabled, or 1 for enabled.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 When the TDE is enabled using **sp_pdw_database_encryption**, the tempdb database is dropped, recreated and encrypted. For that reason, the TDE cannot be enabled on an appliance while there are other active sessions using tempdb. Enabling or disabling TDE on an appliance is an action that changes the state of the appliance, in most cases is expected to be performed once in the appliance lifetime, and should be executed when there is no traffic on the appliance.  
  
## Permissions  
 Requires membership in the **sysadmin** fixed database role, or **CONTROL SERVER** permission.  
  
## Example  
 The following example enables TDE on the appliance.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## See also  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
