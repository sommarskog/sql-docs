---
title: "ListReservedURLs Method (WMI MSReportServer_ConfigurationSetting)"
description: "ListReservedURLs Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "ListReservedURLs method"
---
# ConfigurationSetting Method - ListReservedURLs
  Lists URLs reserved for all applications on the report server.  
  
## Syntax  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## Parameters  
 *Application[]*  
 [out] The applications that have URL reservations.  
  
 *UrlString[]*  
 [out] The URLs that are reserved.  
  
 *Account[]*  
 [out] The account names associated with the account for the URL reservations.  
  
 *AccountSID[]*  
 [out] The account SIDs associated with the account for the URL reservations.  
  
 *Length*  
 [out] The length of the arrays returned by the method.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful; an error code indicates the call was not successful.  
  
## Remarks  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
