---
title: "DatabaseLogonType Property (WMI MSReportServer_ConfigurationSetting)"
description: "DatabaseLogonType Property (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "DatabaseLogonType property"
apilocation: "reportingservices.mof"
apiname: "DatabaseLogonType"
apitype: MOFDef
---
# ConfigurationSetting Property - DatabaseLogonType
  Specifies whether the report server uses a [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows service account, a Windows user account, or a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login to access the report server database. Read-only.  
  
## Syntax  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## Property Values  
 An **integer** object that represents the login type.  
  
## Example Code  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## Remarks  
 Values are:  
  
-   0 for Windows login  
  
-   1 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login  
  
-   2 to log in as a service  
  
 If you specify 0 (Windows), you must set the value in the [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) property to a corresponding a valid Windows user account.  
  
 If you specify 1 (SQL Server), make sure the value of the [DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md) corresponds to a valid [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login.  
  
 If you specify 2 (Windows service), the report server uses an [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] account and the Windows service account to access the report server database. The DatabaseLogonAccount property is ignored.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
