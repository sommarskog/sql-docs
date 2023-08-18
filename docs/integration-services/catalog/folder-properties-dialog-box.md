---
title: "Folder Properties Dialog Box"
description: "Folder Properties Dialog Box"
author: chugugrace
ms.author: chugu
ms.date: "08/26/2016"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.ssis.ssms.isfolderprop.permissions.f1"
  - "sql13.ssis.ssms.iscreatefolder.f1"
  - "sql13.ssis.ssms.isfolderprop.general.f1"
---
# Folder Properties Dialog Box

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A folder contains projects and environments in the **SSISDB** catalog. Each folder defines permissions that apply to the contents of the folder. For more information about [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permissions, see [catalog.grant_permission &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md).  
  
## To Set Folder Description and Permissions  
  
1.  Right-click the folder and select **Properties**.  
  
2.  On the **General** page, select **Description** under **General** and enter an optional description.  
  
3.  On the **Permissions** page, click **Browse...**, select one or more database principals, and click **OK**.  
  
4.  Select a name under **Logins or roles** and specify the appropriate permissions under **Permissions**.  
  
5.  Click **OK** to accept the changes and close the **Folders Properties** dialog box.  
  
## See Also  
 [Integration Services &#40;SSIS&#41; Server](../integration-services-ssis-packages.md)   
 [catalog.grant_permission &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
  
  
