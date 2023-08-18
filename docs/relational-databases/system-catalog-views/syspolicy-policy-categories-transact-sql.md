---
title: "syspolicy_policy_categories (Transact-SQL)"
description: syspolicy_policy_categories (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "syspolicy_policy_categories"
  - "syspolicy_policy_categories_TSQL"
helpviewer_keywords:
  - "syspolicy_policy_groups view"
dev_langs:
  - "TSQL"
---
# syspolicy_policy_categories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Displays one row for each Policy-Based Management policy category in the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Policy categories help you organize policies when you have many policies. The following table describes the columns in the syspolicy_policy_groups view.  
 
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|policy_category_id|**int**|Identifier of the policy category.|  
|name|**sysname**|Name of the policy category.|  
|mandate_database_subscriptions|**bit**|Indicates whether the policy category applies to all databases in an instance without an explicit subscription (1) or the policy category must be applied to a database by using an explicit subscription (0).|  
  
## Remarks  
 Displays a list of Policy-Based Management policy groups.  
  
## Permissions  
 Requires membership in the PolicyAdministratorRole role in the msdb database.  
  
## See Also  
 [Administer Servers by Using Policy-Based Management](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [Policy-Based Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
