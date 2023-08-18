---
title: "View or modify properties of a Policy-Based Management policy"
description: Learn to view or modify the properties of a Policy-Based Management policy for SQL Server using SQL Server Management Studio (SSMS) or Transact-SQL (T-SQL).
author: VanMSFT
ms.author: vanto
ms.date: "10/06/2016"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "Policy-Based Management, modify policies"
  - "Policy-Based Management, view policies"
---
# View or Modify the Properties of a Policy-Based Management Policy
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to view or modify a Policy-Based Management policy's properties in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
  
####  <a name="Permissions"></a> Permissions  
 Requires membership in the PolicyAdministratorRole role in the msdb database.  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To view the properties of all policies on an object  
  
1.  In Object Explorer, right-click a server, server object, database, or database object, point to **Policies** and select **View**. For more information on the available options in the **View Policies -**_object_name_ dialog box, see [View Policies Dialog Box](../../relational-databases/policy-based-management/view-policies-dialog-box.md).  
  
2.  When finished, click **Close**.  
  
#### To view or modify a specific policy's properties  
  
1.  In **Object Explorer**, click the plus sign to expand the server that contains the Policy-Based Management policy that you want to view or modify.  
  
2.  Click the plus sign to expand the **Management** folder.  
  
3.  Click the plus sign to expand **Policy Management**.  
  
4.  Click the plus sign to expand the **Policies** folder.  
  
5.  Right-click the policy that you want to view or modify and select **Properties**. For more information on the available options in the **Open Policy -**_policy_name_ dialog box, see [Create New Policy or Open Policy Dialog Box, General Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) and [Create New Policy or Open Policy Dialog Box, Description Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  When finished, click **OK**.  
  
##  <a name="TsqlProcedure"></a> Using Transact-SQL  
  
#### To view a policy's properties  
  
1.  In **Object Explorer**, connect to an instance of [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  On the Standard bar, click **New Query**.  
  
3.  Copy and paste the following example into the query window and click **Execute**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 For more information, see [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md).  
  
  
