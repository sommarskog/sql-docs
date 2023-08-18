---
title: "DeleteEncryptionKey Method (WMI MSReportServer_ConfigurationSetting)"
description: "DeleteEncryptionKey Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "DeleteEncryptionKey method"
apilocation: "reportingservices.mof"
apiname: "DeleteEncryptionKey (WMI MSReportServer_ConfigurationSetting Class)"
apitype: MOFDef
---
# ConfigurationSetting Method - DeleteEncryptionKey
  Deletes the encryption keys from the report server database.  
  
## Syntax  
  
```vb  
Public Sub DeleteEncryptionKeys(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptionKeys(string InstallationID, out Int32 HRESULT,   
    out string[] ExtendedErrors);  
```  
  
## Parameters  
 *InstallationID*  
 The installation ID of a report server that is in the keys table of the report server database.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
 *ExtendedErrors[]*  
 [out] A string array containing additional errors returned by the call.  
  
## Return Value  
 Returns an HRESULT indicating success or failure of the method call. A value of 0 indicates that the method call was successful. A non-zero value indicates that an error has occurred.  
  
## Remarks  
 The *DeleteEncryptionKey* method deletes entries from the keys table for any report servers that have access to the secure information in the report server database. If the *InstallationID* parameter specified does not correspond to an installation ID in the database, the method returns an error.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
