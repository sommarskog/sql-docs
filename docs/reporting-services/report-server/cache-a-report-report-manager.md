---
title: "Cache a Report (Report Manager)"
description: Learn how to schedule the expiration of a cached report in Report Manager. Caching a report speeds up viewing while it remains cached.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: report-server
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "report execution properties [Reporting Services]"
  - "cache [Reporting Services]"
  - "cached reports [Reporting Services]"
  - "schedules [Reporting Services], report expiration"
  - "expiration [Reporting Services]"
---
# Cache a Report (Report Manager)
  One way to improve performance is to configure caching properties for a report. When a report is cached, a copy of the rendered report is saved for a short period of time. The first user who requests the report must wait for all processing to complete before viewing the report. Subsequent users who request the report within the caching period can view it right away because processing has already occurred.  
  
 There are restrictions on the types of reports that you can cache. For example, a report cannot be cached if report output varies based on the user identity or if data is retrieved using the security token of the user who requests the report. For more information, see [Caching Reports &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### To schedule the expiration of a cached report  
  
1.  Start [Report Manager  &#40;SSRS Native Mode&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  In Report Manager, navigate to the **Contents** page. Navigate to the report for which you want to set caching properties, hover over the item, and click the drop-down arrow.  
  
3.  In the drop-down menu, click **Manage**.  
  
4.  In the left frame, click the **Processing Options**.  
  
5.  On the page, select **Always run this report with the most recent data**.  
  
6.  Select one of the following two cache options and configure expiration as follows:  
  
    -   To configure a cached copy to expire after a particular time period, click **Cache a temporary copy of the report. Expire copy of report after a number of minutes**. Type the number of minutes for report expiration.  
  
    -   To configure a cached copy to expire on a schedule, click **Cache a temporary copy of the report. Expire copy of report on the following schedule.** Click **Configure**, or select a shared schedule to control report expiration  
  
7.  Click **Apply**.  
  
## See Also  
 [Set Report Processing Properties](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Caching Reports &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
