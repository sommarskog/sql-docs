---
title: "Using Reporting Services SOAP Headers"
description: Use Reporting Services SOAP headers to batch operations into a single transaction, manage session state, and retrieve properties based on the path or ID of an item.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/06/2017
ms.service: reporting-services
ms.subservice: report-server-web-service
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "Web service [Reporting Services], SOAP"
  - "Report Server Web service, SOAP"
  - "SOAP headers [Reporting Services]"
  - "SOAP [Reporting Services], headers"
  - "XML Web service [Reporting Services], SOAP"
---
# Using Reporting Services SOAP Headers
  Communication with a Web service method using SOAP follows a standard format. Part of this format is the data that is encoded in an XML document. The XML document consists of a root **Envelope** element, which in turn consists of a required **Body** element and an optional **Header** element. The **Body** element contains the data specific to the message. The optional **Header** element can contain additional information not directly related to the particular message. Each child element of the **Header** element is called a SOAP header.  
  
 Although the SOAP headers can contain data related to the message, they typically contain information processed by the Web server infrastructure.  
  
 The Report Server Web services define several classes for use in the SOAP header: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader>, and <xref:ReportExecution2005.ExecutionHeader>.  
  
## In This Section  
  
|Topic|Description|  
|-----------|-----------------|  
|[Batching Methods](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|Describes how to batch multiple operations into a single transaction using <xref:ReportService2005.BatchHeader>.|  
|[Identifying Execution State](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|Describes how to manage session state in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] using **SessionHeader**.|  
|[Setting the Item Namespace for the GetProperties Method](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|Describes how to retrieve properties based on either the path or the ID of an item by using the <xref:ReportService2010.ReportingService2010.GetProperties%2A> method and the <xref:ReportService2010.ItemNamespaceHeader> SOAP header.|  
  
## See Also  
 [Building Applications Using the Web Service and the .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Technical Reference &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
