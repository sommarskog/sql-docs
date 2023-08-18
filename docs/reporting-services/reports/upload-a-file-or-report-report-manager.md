---
title: "Upload a File or Report in the Report Server"
description: Learn how to add reports and other files to a report server without having to publish those items from a client application.
author: maggiesMSFT
ms.author: maggies
ms.date: 05/24/2018
ms.service: reporting-services
ms.subservice: reports
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "publishing reports [Reporting Services], uploading files"
  - "reports [Reporting Services], publishing"
  - "uploading reports [Reporting Services]"
  - "uploading files [Reporting Services]"
  - "files [Reporting Services], uploading"
---
# Upload a File or Report in the report server
The web portal of the report server provides an upload feature so that you can add reports and other files to a report server without having to publish those items from a client application. Files that you upload from the file system are stored as items on the report server. The type of file you upload determines how it is stored:  
  
-   .rdl files are stored as paginated reports.  
  
-   All other files, including shared data source (.rds) files, are uploaded as resources. Resources are not processed by a report server, but can be viewed in the web portal if the report server supports the MIME type of the file.  
  
### To upload a file or report  
  
1.  In the web portal, click **Upload**.  
  
4.  Browse to the file you want to upload. You can upload a report definition file, an image, a document, or any file that you want to make available on the report server.  
  
5.  Type a name for the new item. An item name can include spaces, but cannot include the reserved characters: \' \" \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|.  
  
6.  If you want to replace an existing item with the new item, select **Overwrite item if it exists**.  
  
7.  Select **OK**.
  
## See Also   
[Create, Modify, and Delete Shared Data Sources](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[Upload Files to a Folder](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
