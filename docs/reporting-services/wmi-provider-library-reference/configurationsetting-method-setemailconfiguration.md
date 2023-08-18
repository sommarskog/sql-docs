---
title: "SetEmailConfiguration Method (WMI MSReportServer_ConfigurationSetting)"
description: "SetEmailConfiguration Method (WMI MSReportServer_ConfigurationSetting)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: wmi-provider-library-reference
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "SetEmailConfiguration method"
apilocation: "reportingservices.mof"
apiname: "SetEmailConfiguration (WMI MSReportServer_ConfigurationSetting Class)"
apitype: MOFDef
---
# ConfigurationSetting Method - SetEmailConfiguration
  Configures the e-mail delivery extension used by the report server to send e-mail.  
  
## Syntax  
  
```vb  
Public Sub SetEmailConfiguration(ByVal SendUsingSMTPServer As Boolean, _  
    ByVal SMTPServer As String, ByVal SenderEmailAddress As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetEmailConfiguration (Boolean SendUsingSMTPServer,   
   string SMTPServer, string SenderEmailAddress,   
   out Int32 HRESULT);  
```  
  
## Parameters  
 *SendUsingSMTPServer*  
 A Boolean value indicating whether the server is to use the SMTP server to send email. This value can only be set to true. Default value is false.  
  
 *SMTPServer*  
 A string containing the name or IP address of an SMTP server.  
  
 *SenderEmailAddress*  
 The e-mail address used in the 'From:' field for e-mails sent from the report server.  
  
 *HRESULT*  
 [out] Value indicating whether the call succeeded or failed.  
  
## Return Value  
 Returns an *HRESULT* indicating success or failure of the method call. A value of 0 indicates that the method call was successful. A non-zero value indicates that an error has occurred.  
  
## Remarks  
 When the *SendUsingSMTPServer* parameter is set to **true**, the **SendUsing** entry in the report server configuration file is set to 1. When *SendUsingSMTPServer* is set to **false**, the **SendUsing** entry is not configured.  
  
 This method does not provide a way for users to set the **SendUsing** entry in the report server configuration file to a value other than 1. To configure the report server for anything other than SMTP mail, you must edit the configuration file manually.  
  
## Requirements  
 **Namespace:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## See Also  
 [MSReportServer_ConfigurationSetting Members](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
