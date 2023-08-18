---
title: "Using Secure Web Service Methods"
description: Require a secure connection for Report Server Web service methods with the SecureConnectionLevel setting in the RSReportServer configuration file.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/06/2017
ms.service: reporting-services
ms.subservice: report-server-web-service
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "SOAP [Reporting Services], secure connections"
  - "Web service [Reporting Services], SOAP"
  - "Report Server Web service, SOAP"
  - "XML Web service [Reporting Services], SOAP"
---
# Using Secure Web Service Methods
  Certain Report Server Web service methods may require a secure connection when you invoke them. The methods that require a secure connection are determined by the **SecureConnectionLevel** setting in the RSReportServer.config file. The value of the setting is an integer value with a valid range of 0 and higher. The following table describes these values.  
  
|Level|Description|  
|-----------|-----------------|  
|**0**|Not secure. Calls made to the Reporting Services SOAP API do not require a secure connection.|  
|Greater than **0**|Secure. All calls made to the Reporting Services SOAP API require a secure connection.|  
  
 You can use the <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> method of the Web service to return a list of Web service methods that require a secure connection according to the current configuration of the report server. In a TLS scenario, you should evaluate the list of methods that are returned by <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> and change the scheme name of the Web service URI to "https" or "http" depending on the method being called.  
  
## See Also  
 [Building Applications Using the Web Service and the .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Report Server Web Service](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
