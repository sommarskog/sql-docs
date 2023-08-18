---
title: "Omitting Values for Optional Web Service Objects"
description: Some properties of Report Server Web service complex types support the Specified property, which allows you to omit a value for some writable properties.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/04/2017
ms.service: reporting-services
ms.subservice: report-server-web-service
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "Web service [Reporting Services], omitted values"
  - "XML Web service [Reporting Services], omitted values"
  - "Report Server Web service, omitted values"
  - "omitting values [Reporting Services]"
---
# Omitting Values for Optional Web Service Objects
  Properties of several of the Report Server Web service complex types have an accompanying property known as the Specified property. The name of the property consists of the original property name with the word "Specified" appended to it. The presence of this property indicates that a value for the original property may sometimes be omitted. This is a direct result of the translation from the Web Service Description Language (WSDL) to a [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proxy class. For example, the Web service property <xref:ReportService2010.DataSourceDefinition.Enabled%2A> of the complex type <xref:ReportService2010.DataSourceDefinition> has an accompanying property named <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A>. If you are building an application and do not want to set a value for the <xref:ReportService2010.DataSourceDefinition.Enabled%2A> property, you do not have to supply a value for <xref:ReportService2010.DataSourceDefinition.Enabled%2A>; the default value of **true** is used. However, you still need to set <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> to **false**. If you supply a value for the <xref:ReportService2010.DataSourceDefinition.Enabled%2A> property, you need to set <xref:ReportService2010.DataSourceDefinition.EnabledSpecified%2A> equal to **true**. This is the case for writable properties. For read-only properties, you do not need to take any action.  
  
> [!IMPORTANT]  
>  Failure to specify a property using the above-mentioned technique can result in unpredictable Web service behavior.  
  
 The data types that usually require you to handle the additional Specified property are **Boolean**, **DateTime**, and **Enumeration**.  
  
 For an example, see <xref:ReportService2010.ReportingService2010.CreateDataSource%2A> method.  
  
## See Also  
 [Building Applications Using the Web Service and the .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Technical Reference &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
