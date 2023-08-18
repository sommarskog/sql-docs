---
title: "CreateSSLCertificateBinding Method (WMI MSReportServer_ConfigurationSetting)"
description: "CreateSSLCertificateBinding Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "CreateSSLCertificateBinding"
---
# ConfigurationSetting Method - CreateSSLCertificateBinding
  Creates a TLS/SSL Certificate binding.  
  
## Syntax  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## Parameters  
 *Application*  
 The name of application that the certificate binding should be created for.  
  
 *CertificateHash*  
 The hash for the certificate.  
  
 *IPAddress*  
 The IP address for the application.  
  
 *Port*  
 The TLS port associated with the binding.  
  
 *Lcid*  
 The locale to use for the error messages returned.  
  
 *Error*  
 [out] The description of the errors that occurred.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful; an error code indicates the call was not successful.  
  
## Remarks  
 This method adds a binding to rsreportserver.config for the application. If a binding does not already exist in HTTP.SYS, it is created there.  
  
 Before creating the binding, the method call examines the Url Reservations for the specified application to determine if the TLS/SSL Certificate Binding is valid.  
  
 The following conditions are validated and can result in errors:  
  
1.  Certificate does not exist.  
  
2.  The IPAddress specified does not correspond to an IPAddress of this computer.  
  
3.  The IPAddress specified is a DHCP IPAddress (changes periodically) - use the Wildcard IP address instead (0.0.0.0).  
  
4.  IPAddress specified does not match the IP address of a URL reservations AND neither a wildcard or host name URL reservation exist.  
  
5.  A URL reservation that specifies a host name exists, but the host name does not match the certificate host name.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
