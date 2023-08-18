---
title: "sp_set_firewall_rule (Azure SQL Database)"
description: "sp_set_firewall_rule (Azure SQL Database)"
author: VanMSFT
ms.author: vanto
ms.date: "07/28/2016"
ms.service: sql-database
ms.topic: "reference"
f1_keywords:
  - "sp_set_firewall_rule"
  - "sp_set_firewall_rule_TSQL"
  - "sys.sp_set_firewall_rule"
  - "sys.sp_set_firewall_rule_TSQL"
helpviewer_keywords:
  - "sp_set_firewall_rule"
  - "firewall_rules, setting server rules"
dev_langs:
  - "TSQL"
monikerRange: "= azuresqldb-current || = azure-sqldw-latest"
---
# sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  Creates or updates the server-level firewall settings for your [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. This stored procedure is only available in the master database to the server-level principal login or assigned Azure Active Directory principal.  
  
  
## Syntax  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## Arguments  
 The following table demonstrates the supported arguments and options in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)].  
  
|Name|Datatype|Description|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR(128)**|The name used to describe and distinguish the server-level firewall setting. The value passed in must match this parameter's data type (NVARCHAR).|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR(50)**|The lowest IP address in the range of the server-level firewall setting. IP addresses equal to or greater than this can attempt to connect to the [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. The lowest possible IP address is `0.0.0.0`.|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR(50)**|The highest IP address in the range of the server-level firewall setting. IP addresses equal to or less than this can attempt to connect to the [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server. The highest possible IP address is `255.255.255.255`.<br /><br /> Note: Azure connection attempts are allowed when both this field and the *start_ip_address* field equals `0.0.0.0`.|  
  
## Remarks  
 The names of server-level firewall settings must be unique. If the name of the setting provided for the stored procedure already exists in the firewall settings table, the starting and ending IP addresses will be updated. Otherwise, a new server-level firewall setting will be created.  
  
 When you add a server-level firewall setting where the beginning and ending IP addresses are equal to `0.0.0.0`, you enable access to your [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server from Azure. Provide a value to the *name* parameter that will help you remember what the server-level firewall setting is for.  
  
 In [!INCLUDE[ssSDS](../../includes/sssds-md.md)], login data required to authenticate a connection and server-level firewall rules are temporarily cached in each database. This cache is periodically refreshed. To force a refresh of the authentication cache and make sure that a database has the latest version of the logins table, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
 
This is an extended stored procedure, so the data type of the value passed in for each parameter must match the parameter definition.
  
## Permissions  
 Only the server-level principal login created by the provisioning process or an Azure Active Directory principal assigned as admin can create or modify server level firewall rules. The user must be connected to the master database to execute sp_set_firewall_rule.  
  
## Examples  
 The following code creates a server-level firewall setting called `Allow Azure` that enables access from Azure. Execute the following in the virtual master database.  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 The following code creates a server-level firewall setting called `Example setting 1` for only the IP address `0.0.0.2`. Then, the `sp_set_firewall_rule` stored procedure is called again to update the end IP address to `0.0.0.4`, in that firewall setting. This creates a range which allows IP addresses `0.0.0.2`, `0.0.0.3`, and `0.0.0.4` to access the server.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## See Also  
 [Azure SQL Database Firewall](/azure/azure-sql/database/firewall-configure)   
 [How to: Configure Firewall Settings (Azure SQL Database)](/azure/azure-sql/database/firewall-configure)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
