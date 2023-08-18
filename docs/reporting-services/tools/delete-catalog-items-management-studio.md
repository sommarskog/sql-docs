---
title: "Delete Catalog Items (Management Studio)"
description: Learn about the options on the Delete Catalog Items page of Management Studio that allow you to delete shared schedules and role definitions.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: tools
ms.topic: conceptual
ms.custom: updatefrequency5
f1_keywords:
  - "sql13.swb.reportserver.deleteitems.f1"
---
# Delete Catalog Items (Management Studio)
  Use this page to delete shared schedules and role definitions.  
  
 If you delete a shared schedule that is used by multiple reports and subscriptions, the report server will create individual schedules for each report and subscription that previously used the shared schedule. Each new individual schedule will contain the date, time, and recurrence pattern that was specified in the shared schedule. Note that [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] does not provide central management of individual schedules. If you delete a shared schedule, you will now need to maintain the schedule information for each individual item. Before deleting a shared schedule, use the [Reports page](../../reporting-services/tools/schedule-properties-reports-page.md) to determine which reports are currently using the shared schedule.  
  
 For role definitions, you can only delete those that are not actively used in a role assignment. If you try to delete a role that is currently in use, the report server will not delete the role and you will see an error message to that effect. If this page contains a single role definition that is not currently in use, it will be deleted when you click **OK**. If this page contains multiple roles, you cannot select which roles to keep or remove. All unused role definitions will be deleted when you click **OK**.  
  
 You cannot undo a delete operation. If you want to recover an item that you deleted, you must either recreate it or restore a backup copy of the report server database.  
  
## Options  
 **Name**  
 Specifies the name of the item you are deleting.  
  
 **Type**  
 Shows the type of item you are deleting.  
  
 **Owner**  
 Shows the name of the owner. In most cases, this is System.  
  
 **Status**  
 Shows progress information for a delete operation.  
  
 **Error**  
 Displays an error code if an error occurs while deleting an item.  
  
## See Also  
 [Delete an Item &#40;Management Studio&#41;](../../reporting-services/tools/delete-an-item-management-studio.md)   
 [Report Server in Management Studio F1 Help](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)  
  
  
