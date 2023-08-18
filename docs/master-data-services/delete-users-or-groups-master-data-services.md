---
title: Delete Users or Groups
description: "Delete Users or Groups (Master Data Services)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
helpviewer_keywords:
  - "deleting groups [Master Data Services]"
  - "groups [Master Data Services], deleting"
  - "users [Master Data Services], deleting"
  - "deleting users [Master Data Services]"
---
# Delete Users or Groups (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Delete users or groups when you no longer want them to access [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Note the following behavior when deleting users and groups:  
  
-   If you delete a user who is a member of a group that has access to [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], then the user can still access [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] until you remove the user from the Active Directory or local group.  
  
-   If you delete a group, all users from the group who have accessed [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] are displayed in the **Users** list until you delete them.  
  
-   Changes to security are not propagated to the MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] for 20 minutes.  
  
## Prerequisites  
 To perform this procedure:  
  
-   You must have permission to access the **Users and Group Permissions** functional area.  
  
### To delete users or groups  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], click **User and Group Permissions**.  
  
2.  To delete a user, remain on the **Users** page. To delete a group, from the menu bar, click **ManageGroups.**  
  
3.  In the grid,select the row for the user or group that you want to delete.  
  
4.  Click **Delete selected user** or **Delete selected group**.  
  
5.  On the confirmation dialog box, click **OK**.  
  
## See Also  
 [Security &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
