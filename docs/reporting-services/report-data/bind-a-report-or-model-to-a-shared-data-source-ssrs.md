---
title: "Bind a Report to a Shared Data Source"
description: Learn how to bind a report to a shared data source on a report server that is running in native mode or SharePoint integrated mode.
author: maggiesMSFT
ms.author: maggies
ms.date: 05/24/2018
ms.service: reporting-services
ms.subservice: report-data
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "shared data sources [Reporting Services]"
  - "data sources [Reporting Services], shared"
---
# Bind a Report to a Shared Data Source (SSRS)
  In some situations, such as when you move a report from a test server to a production server, you might want to save the file to your local computer and then upload it to a different report server. When you upload the report to the new server, you need to rebind it to a shared data source that is stored on the new report server. If you don't rebind the report, it will not work correctly when accessed from the new report server.  
  
> [!IMPORTANT]  
>  Before rebinding a report to a shared data source, the data source must already exist on the report server or SharePoint library. For more information about data sources, see [Create, Modify, and Delete Shared Data Sources &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## To bind a report to a shared data source on a report server running in native mode  
  
1.  In the web portal, click the ellipsis (...) in the upper-right corner of the report tile > **Manage**.  

2.  Click **Data Sources**.  
  
3.  Click **A shared data source**, then navigate to the data source to which you want to bind the report.  
  
4.  Select the data source and then click **Save**.  
  
5.  Click **Apply**.  
  
     The report is now bound to the data source that you selected.  
  
## To bind a report to a shared data source on a report server running in SharePoint integrated mode  
  
1.  If the library is not already open, click its name on the Quick Launch bar. If the name of your library does not appear, click **View All Site Content**, and then click the name of your library.  
  
2.  Point to the report and click the down arrow.  
  
3.  Click **Manage Data Sources**.  
  
4.  Click **dataSource1**.  
  
5.  In the **Connection Type** area, verify that **Shared data source** is selected.  
  
6.  In the **Data Source Link** area, click the ellipsis (...) button.  
  
7.  Locate the data source you want to use.  
  
8.  Select the data source and **click OK**.  
  
9.  Select **OK**.
  
10. Click **Close**.  
  
## See Also  
 [Upload Documents to a SharePoint Library &#40;Reporting Services in SharePoint Mode&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Create and Manage Shared Data Sources &#40;Reporting Services in SharePoint Integrated Mode&#41;](/previous-versions/sql/)   
 [Create data connection strings - Report Builder & SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Data Sources Supported by Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
