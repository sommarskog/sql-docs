---
title: "Limit Report History - Reporting Services"
description: Learn how to configure the report history for a report server. Also learn how to configure report history for a specific report.
author: maggiesMSFT
ms.author: maggies
ms.date: 06/26/2019
ms.service: reporting-services
ms.subservice: reports
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "viewing report history"
  - "report history [Reporting Services], viewing history"
  - "report history [Reporting Services], configuring history"
  - "historical data [Reporting Services]"
  - "displaying report history"
---
# Limit Report History - Reporting Services
  Report history is a collection of report snapshots that you create over time. You can create report history on demand, or schedule how often a snapshot is created and added to report history.  
  
 Report history is stored in the report server database. If report snapshots contain a large amount of data, you might consider limiting report history to minimize the effect of snapshot retention on database size.  

::: moniker range="=sql-server-2016"
  
## To configure report history for a report server  
  
1.  In Report Manager, click **Site Settings** on the global toolbar.  
  
2.  Select **Keep an unlimited number of snapshots in report history** if you want to keep all report history indefinitely. Otherwise, select **Limit the copies of report history** to specify the maximum number of snapshots that can be kept for any given report.  
  
3.  Click **Apply**.  
  
## To configure report history for a specific report  
  
1.  In Report Manager, navigate to the report for which you want to configure history, and then click the report to open it.  
  
2.  Click the **Properties** tab.  
  
3.  Click the **History** tab.  
  
4.  Select the options for your report and click **Apply**. For details about each option, see [Snapshot Options Properties Page &#40;Report Manager&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## See Also  
 [Add a Snapshot to Report History &#40;Report Manager&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Report Manager  &#40;SSRS Native Mode&#41;](../web-portal-ssrs-native-mode.md)  

::: moniker-end

::: moniker range=">=sql-server-2017"

## To configure report history for a report server  
  
1.  In the web portal, click **Site Settings** on the global toolbar.  
  
2.  Select **Keep an unlimited number of snapshots in report history** if you want to keep all report history indefinitely. Otherwise, select **Limit the copies of report history** to specify the maximum number of snapshots that can be kept for any given report.  
  
3.  Click **Apply**.  
  
## To configure report history for a specific report  
  
1.  In the web portal, navigate to the report for which you want to configure history, and then click the report to open it.  
  
2.  Click the **Properties** tab.  
  
3.  Click the **History** tab.  
  
4.  Select the options for your report and click **Apply**. For details about each option, see [Snapshot Options Properties Page](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).  
  
## See Also  
 [Add a Snapshot to Report History](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
