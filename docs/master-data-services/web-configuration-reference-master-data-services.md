---
title: Web Configuration Reference
description: "Web Configuration Reference (Master Data Services)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
helpviewer_keywords:
  - "web configuration file [Master Data Services]"
---
# Web Configuration Reference (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] uses a Web.config file to contain the configuration settings that enable Internet Information Services (IIS) to host the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web application and the Web service. This Web.config file is located in the WebApplication folder of the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] installation path. For more information about the path and permissions, see [Folder and File Permissions &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## Web.Config Elements  
 The Web.config file contains a custom [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] element, **\<masterDataServices>**, in addition to standard IIS, .NET Framework, ASP.NET, and Windows Communication Foundation (WCF) configuration elements. The following table describes the elements included in the Web.config file.  
  
|Configuration Element|Description|  
|---------------------------|-----------------|  
|**masterDataServices**|Custom element. Connects the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web service to a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.|  
|**connectionStrings**|ASP.NET element. For more information, see [connectionStrings Element (ASP.NET Settings Schema)](/previous-versions/dotnet/netframework-4.0/bf7sd233(v=vs.100)) in the MSDN Library.|  
|**system.web**|ASP.NET element. For more information, see [system.web Element (ASP.NET Settings Schema)](/previous-versions/dotnet/netframework-4.0/dayb112d(v=vs.100)) in the MSDN Library.|  
|**startup**|.NET Framework element. For more information, see [\<startup> Element](/dotnet/framework/configure-apps/file-schema/startup/startup-element) in the MSDN Library.|  
|**runtime**|.NET Framework element. For more information, see [\<runtime> Element](/dotnet/framework/configure-apps/file-schema/runtime/runtime-element) in the MSDN Library.|  
|**system.codedom**|.NET Framework element. For more information, see [\<system.codedom> Element](/dotnet/framework/configure-apps/file-schema/compiler/system-codedom-element) in the MSDN Library.|  
|**system.web.extensions**|ASP.NET element. For more information, see [system.web.extensions Element (ASP.NET Settings Schema)](/previous-versions/dotnet/netframework-4.0/bb546044(v=vs.100)) in the MSDN Library.|  
|**system.webServer**|Section group that contains IIS elements. For more information, see [system.webServer Section Group \[IIS 7 Settings Schema\]](/previous-versions/iis/settings-schema/ms689429(v=vs.90)) in the MSDN Library.|  
|**system.serviceModel**|WCF element. For more information, see [\<system.serviceModel>](/dotnet/framework/configure-apps/file-schema/wcf/system-servicemodel) in the MSDN Library.|  
|**system.diagnostics**|.NET Framework element. For more information, see [\<system.diagnostics> Element](/dotnet/framework/configure-apps/file-schema/trace-debug/system-diagnostics-element) in the MSDN Library.|  
|**appSettings**|ASP.NET element. For more information, see [appSettings Element (General Settings Schema)](/previous-versions/dotnet/netframework-4.0/ms228154(v=vs.100)) in the MSDN Library.|  
  
## masterDataServices Element  
 The **\<masterDataServices>** element is a custom element that is used to connect a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web service to a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.  
  
### Syntax  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### Elements and Attributes  
  
|Item|Description|  
|----------|-----------------|  
|**instance**|Child element. Contains attributes that specify information for the Web service and database connection string.|  
|**virtualPath**|Attribute. Specifies the virtual path of the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web application and service. This corresponds to the **path** attribute of the **\<application>** element under the **\<site>** element in the IIS ApplicationHost.config file.|  
|**siteName**|Attribute. Specifies the name of the site that hosts the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web application and service. This corresponds to the **name** attribute of the **\<site>** element under **\<sites>** in the IIS ApplicationHost.config file.|  
|**connectionName**|Attribute. Specifies the name of the connection to use. This corresponds to the **name** attribute of the **\<add>** element under the **\<connectionStrings>** element in Web.config.|  
|**serviceName**|Attribute. Specifies the name of the Web service. This corresponds to the **name** attribute of the **\<service>** element under the **\<services>** element in Web.config.|  
  
### Example  
 The following example demonstrates a service named MDS1 on the Contoso site and /MDS path using a connection string specified by MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
