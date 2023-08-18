---
title: "rsServerConfigurationError - Reporting Services Error"
description: "In this error reference page, learn about event ID 'rsServerConfigurationError': The report server has encountered a configuration error."
author: maggiesMSFT
ms.author: maggies
ms.date: 03/20/2017
ms.service: reporting-services
ms.subservice: troubleshooting
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "rsServerConfigurationError"
---
# rsServerConfigurationError - Reporting Services Error
    
## Details  
  
|Category|Value|  
|-|-|  
|Product Name|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Event ID|rsServerConfiguration|  
|Event Source|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Component|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Message Text|The report server has encountered a configuration error.|  
  
## Explanation  
 This is a general purpose error that occurs when either the report server or a report authoring tool has invalid configuration settings. The error is usually accompanied by a second message that states the actual cause of the error.  
  
 The following list summarizes possible causes:  
  
-   The RSReportServer.config or RSReportDesigner.config file cannot be found or read.  
  
-   XML elements in either configuration file are missing or invalid.  
  
-   Values for one or more XML elements are missing or invalid.  
  
-   Registry settings are invalid.  
  
## User Action  
 If this error began to occur after you manually edited a configuration file, remove your changes and enter the previous value, or restore a previous version if you have a backup.  
  
 To review additional error message information that accompanies the **rsServerConfiguration** error, review the report server trace log files, which are located at \Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles. For more information, see [Reporting Services Log Files and Sources](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## Internal-Only  
  
## See Also  
 [Reporting Services Configuration Files](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Modify a Reporting Services Configuration File &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
