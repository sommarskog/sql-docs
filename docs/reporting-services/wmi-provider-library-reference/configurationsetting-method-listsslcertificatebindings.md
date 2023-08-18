---
title: "ListSSLCertificateBindings Method (WMI MSReportServer_ConfigurationSetting)"
description: "ListSSLCertificateBindings Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "ListSSLCertificateBindings method"
---
# ConfigurationSetting Method - ListSSLCertificateBindings
  Returns a list of installed TLS/SSL certificates on the computer.  
  
## Syntax  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## Parameters  
 *LCID*  
 The locale to use for the error messages that are returned.  
  
 *Application[]*  
 [out] The applications that have certificate bindings.  
  
 *CertificateHash[]*  
 [out] The hashes for the certificates.  
  
 *IPAddress[]*  
 [out] The IP address for the applications.  
  
 *Port[]*  
 [out] The port number stored in the binding in rsreportserver.config.  
  
 *Errors[]*  
 [out] The descriptions for errors that occurred.  
  
 *Length*  
 [out] The length of the array returned by the method.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful. A non-zero value indicates that an error has occurred.  
  
## Remarks  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
