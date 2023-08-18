---
title: "URL Reservation Syntax  (Configuration Manager)"
description: "URL Reservation Syntax  (Report Server Configuration Manager)"
author: maggiesMSFT
ms.author: maggies
ms.date: 10/05/2022
ms.service: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "URL reservations"
---
# URL Reservation Syntax  (Report Server Configuration Manager)
  This topic describes the parts of the URL string for the Report Server Web service and Report Manager. The URL string that is stored internally has a different structure from a URL that you type in the Address bar of a browser window. The URL reservation string appears in the Results window of the Reporting Services Configuration tool when you configure a URL and in the RSReportServer.config file. Knowing how the URL string is defined can be useful if you are troubleshooting URL reservation problems or querying HTTP.SYS to view the internal URL reservations that are defined on your server.  
  
## URL Syntax  
 A report server URL is stored in the **UrlString** element and the **VirtualDirectory** element. The reason for separating **UrlString** and **VirtualDirectory** into separate elements is that you can have multiple URL strings, but only one virtual directory name for each [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] application.  
  
 In HTTP.SYS, the URL reservation includes both the **UrlString** and **VirtualDirectory**. The syntax for a URL reservation has the following parts:  
  
 \<scheme>://\<hostname>:\<port>/\<virtualdirectory>  
  
 The following table describes each property and which values are valid for each one.  
  
|Property|Valid values|Description|  
|--------------|------------------|-----------------|  
|Scheme|http or https|Prefixes for non-TLS and TLS connections.|  
|Hostname| | Identifies the server on the network.|
| |(+) Strong wildcard, equates to **(All Assigned)** value for the IP address. | (+) Strong wildcard is the default. HTTP.SYS will accept all requests on all network adapters for a given port and virtual directory combination. The report server will accept any request on the port.|
| | (\*) Weak wildcard, equates to an IP address of **(All Unassigned)**. | (\*) Weak wildcard. HTTP.SYS accepts all requests not handled by other URL reservations on all network adapters for a given port and virtual directory combination.|
| | Fully qualified domain name | Fully qualified domain name includes domain address and server name, as registered with a domain controller or public domain name server.|
| | Machine name | Machine name is the NETBIOS name of the computer on the network.|
| | IP address (IPV4)| IP address (IPV4) is the IP address of a network adapter on the computer in IPV4 format: *nnn.nnn.nnn.nnn*.|
| | IP address (IPV6) | IP address (IPV6) is the IP address of a network adapter on the computer in IPV6 format: \<header>:\<header>:*nnn.nnn.nnn.nnn*.| 
|Port|80 | Port 80 is the standard port for HTTP requests to and from a server.|
| |443 |Port 443 is the standard report for TLS connections.|
| |\<custom>| You can use any port that is not already reserved by another application.|
|Virtualdirectory|ReportServer*[_InstanceName]| Specifies the name of the application. This value is a string. By default, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] uses ReportServer and Reports as the application names for the Report Server Web service and Report Manager applications. You can use different names if you prefer.|
| |*Reports*[_InstanceName]* | This value is required. It identifies the application.|
| |\<custom>|Specify only one virtual directory for each application instance. To create multiple URLs for the same application in the same instance, create multiple versions of the **UrlString**. To create unique virtual directory names for multiple application instances, consider including the instance name in the virtual directory name, using the underscore character (_) to append the instance name. *InstanceName* is optional, but recommended if you have multiple instances on the same computer. For more information about how to set URL reservations for named instances, see [URL Reservations for Multi-Instance Report Server Deployments  &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).<br /><br /> The value for virtual directory is not case-sensitive. You can use any string as long as it does not include URL separator characters or URL encoding.|  
  
## See Also  
 [Configure Report Server URLs  &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configure a URL  &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
