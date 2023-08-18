---
title: "Reporting Services WMI Provider Library Reference"
description: "Reporting Services WMI Provider Library Reference (SSRS)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "WMI provider [Reporting Services], library"
apilocation: "reportingservices.mof"
apiname: "Reporting Services WMI Provider Library"
---
# Reporting Services WMI Provider Library Reference (SSRS)
  The [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows Management Instrumentation (WMI) provider supports WMI operations that enable you to write scripts and code to modify settings of the report server and Report Manager.  
  
 For example, if you want to change whether integrated security is used when the report server connects to the report server database, create an instance of the MSReportServer_ConfigurationSetting class and use the DatabaseIntegratedSecurity property of the of the report server instance. The classes shown in the following table represent [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] components. The classes are defined in either the [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] or the [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] namespaces. Each of the classes support read and write operations. Create operations are not supported.  
  
## Classes  
 [MSReportServer_Instance Class](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 Provides basic information required for a client to connect to an installed report server.  
  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 Represents the installation and run-time parameters of a report server instance. These parameters are stored in the configuration file for the report server.  
  
 For more information about WMI operations, see the WMI SDK documentation included with the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## See Also  
 [Access the Reporting Services WMI Provider](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Technical Reference &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
