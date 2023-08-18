---
title: "DeleteEncryptedInformation Method (WMI MSReportServer_ConfigurationSetting)"
description: "DeleteEncryptedInformation Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "DeleteEncryptedInformation method"
apilocation: "reportingservices.mof"
apiname: "DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)"
apitype: MOFDef
---
# ConfigurationSetting Method - DeleteEncryptedInformation
  Deletes the encrypted information from the report server database.  
  
## Syntax  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## Parameters  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
 *ExtendedErrors[]*  
 [out] A string array containing additional errors returned by the call.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful. A non-zero value indicates that an error has occurred.  
  
## Remarks  
 When this method is invoked, the following data is deleted:  
  
-   Data source information that is encrypted, including user name and password.  
  
-   Subscription data that is encrypted using the delivery extension interfaces.  
  
-   All the information from the keys table in the report server database.  
  
 After this method is invoked, the user must initialize each computer that uses the report server database.  
  
 Calling the DeleteEncryptedInformation method does not affect the report server configuration file.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
