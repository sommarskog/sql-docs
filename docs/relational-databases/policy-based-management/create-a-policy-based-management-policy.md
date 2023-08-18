---
title: "Create a Policy-Based Management Policy"
description: "Create a Policy-Based Management Policy"
author: VanMSFT
ms.author: vanto
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "Policy-Based Management, creating policies"
---
# Create a Policy-Based Management Policy
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to create a Policy-Based Management policy in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **In This Topic**  
  
-   **Before you begin:**  
  
     [Security](#Security)  
  
-   **To create a policy, using:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 Requires membership in the PolicyAdministratorRole role in the msdb database.  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To create a policy  
  
1.  In **Object Explorer**, click the plus sign to expand the server where you want to create a new a Policy-Based Management policy.  
  
2.  Click the plus sign to expand the **Management** folder.  
  
3.  Click the plus sign to expand **Policy Management**.  
  
4.  Right-click the **Policies** folder and select **New Policy**.  
  
5.  In the **Create New Policy** dialog box, in the **Name** box, type the name of the new policy.  
  
6.  If you want the policy to be enabled as soon as it is created, select the **Enabled** check box. If the evaluation mode is **On demand**, the **Enabled** check box is not available.  
  
7.  In the **Check condition** list, select one of the existing conditions, or select **New Condition**. To edit a condition, select the condition and then click the ellipsis (**...**). For more information, see [Create a New Policy-Based Management Condition](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) or [View or Modify the Properties of a Policy-Based Management Condition](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md).  
  
8.  In the **Against targets** box, select one or more target types for this policy. Some conditions and facets can only be applied to certain types of targets. The available target sets appear in the associated box. Expand **Every** to select a filtering condition for some types of the targets. If no targets appear in this box, the check condition is scoped at the server level.  
  
9. In the **Evaluation Mode** box, select how this policy will behave. Different conditions can have different valid evaluation modes. For more information about which evaluation modes are valid, see [Administer Servers by Using Policy-Based Management](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
10. If the policy will be evaluated on a schedule, set the evaluation mode to **On schedule**, and then click **Pick** to select a schedule, or click **New** to create a new schedule.  
  
11. To limit the policy to subset of the target types, in the **Server restriction** box, select from limiting conditions or create a new condition.  
  
     For more information on the available options in the **Create New Policy** dialog box, see [Create New Policy or Open Policy Dialog Box, General Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) or [Create New Policy or Open Policy Dialog Box, Description Page](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
12. When finished click **OK**.  

