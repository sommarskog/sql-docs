---
title: "Set the Language for Report Parameters in a URL"
description: "Learn how to set the language for report parameters in a URL by using the rs:ParameterLanguage URL access parameter."
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "overriding report language settings"
  - "report servers [Reporting Services], language settings"
  - "languages [Reporting Services]"
  - "URL access [Reporting Services], language overrides"
  - "international considerations [Reporting Services]"
  - "global considerations [Reporting Services]"
---
# Set the Language for Report Parameters in a URL
  The *rs:ParameterLanguage* URL access parameter alleviates a problem in which culture-sensitive report parameters, such as dates, times, currency, and numbers, are interpreted using the browser language. With *rs:ParameterLanguage*, the URL is now interpreted independently of the browser. For example, if the report server is set to a regional setting of German, but a user is accessing a report via a URL using a browser that is set to English-United States, parameter values that are passed to a report server will be misinterpreted.  
  
 Consider the following URL to a report:  
  
```  
https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008  
```  
  
 In the above case, the server, running under a culture of "de-de", generates a URL either through an e-mail subscription or a hyperlink. The hyperlink indicates that the report should be parameterized by a start date of October 4, 2008 and an end date of October 11, 2008 according to German date/time standards. However, a user that is accessing the URL through a browser set to "en-us" forces the server to interpret the values as April 10, 2008 and November 10, 2008 under United States English date/time standards. To fix the problem, *rs:ParameterLanguage* can be used to override the browser language for parameter interpretation:  
  
```  
https://myrshost/Reportserver?/SampleReports/Product+Line+Sales&rs:Command=Render&StartDate=4/10/2008&EndDate=11/10/2008&rs:ParameterLanguage=de-DE  
```  
  
 In addition to a value of **true** and **false** for the URL access parameter *rc:Parameters*, you can now pass a value of **Collapsed**. When using *rc:Parameters*=**Collapsed** on a URL, the parameter prompt area of the HTML viewer is collapsed out of sight, but can still be toggled by the user. A value of **false** removes the parameter prompt area from the HTML viewer toolbar and makes it unavailable to the end-user.  
  
## See Also  
 [URL Access &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL Access Parameter Reference](../reporting-services/url-access-parameter-reference.md)  
  
  
