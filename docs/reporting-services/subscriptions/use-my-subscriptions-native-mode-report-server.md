---
title: "Use My Subscriptions (Native Mode Report Server)"
description: Learn to use the My Subscriptions page in the Reporting Services web portal to view, modify, enable, disable, or delete existing subscriptions.
author: maggiesMSFT
ms.author: maggies
ms.date: 07/01/2016
ms.service: reporting-services
ms.subservice: subscriptions
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "subscriptions [Reporting Services], My Subscriptions page"
  - "My Subscriptions page [Reporting Services]"
---
# Use My Subscriptions (Native Mode Report Server)
The [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web portal includes a **My Subscriptions** page that organizes all of your subscriptions into one place. You can use *My Subscriptions* to view, modify, enable, disable, and delete existing subscriptions. However, you cannot use it to create subscriptions.  My Subscriptions shows only the subscriptions that you create. It does not list subscriptions that are owned by other users, even if you are added as a subscriber to those subscriptions, nor does it show data-driven subscriptions.
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Native mode|  
  
The search field will dynamically filter the list of subscriptions as youYou cannot search for subscriptions by name, nor can you search for subscriptions based on trigger information, status information, and so forth. For more information, see [Create and Manage Subscriptions for Native Mode Report Servers](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).
  
## To open the My Subscriptions page  
1. Open the [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web portal.
2. Click settings ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) in the toolbar.
3. Click **My Subscriptions**.

For more information, see [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).

## Use Windows PowerShell to list MySubscriptions  
 ![PowerShell related content](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell related content")  
  
 The following PowerShell script will return the list of subscriptions and subscription properties for the current user. For more information, see [ReportingService2010.ListMySubscriptions Method](/dotnet/api/reportservice2010.reportingservice2010.listmysubscriptions).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## See Also  
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Subscriptions and Delivery &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [old_Create and Manage Subscriptions for Native Mode Report Servers](./create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
