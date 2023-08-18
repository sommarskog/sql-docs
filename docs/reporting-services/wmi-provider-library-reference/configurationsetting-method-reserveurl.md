---
title: "ReserveURL Method (WMI MSReportServer_ConfigurationSetting)"
description: "ReserveURL Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "ReservedURL method"
---
# ConfigurationSetting Method - ReserveURL
  Adds a URL reservation for a given application.  
  
## Syntax  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## Parameters  
 *Application*  
 The name of application to reserve the URL for.  
  
 *URLString*  
 The URL for the reservation.  
  
 *lcid*  
 The locale to use for the error messages returned.  
  
 *Error*  
 [out] The description of the error that occurred.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful; an error code indicates the call was not successful.  
  
## Remarks  
 *UrlString* does not include the virtual directory name. The [SetVirtualDirectory](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) method is provided for that purpose.  
  
 URL reservations are created for the current Windows service account. Changing the Windows service account requires updating all the URL reservations manually.  
  
 This method causes all application domains to hard recycle. Application domains are restarted after this operation is complete.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
