---
title: "Best Practices for Reporting Services Exception Handling"
description: Learn about best practices for Reporting Services exception handling, such as how to deal with error cases that do not throw exceptions.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/06/2017
ms.service: reporting-services
ms.subservice: report-server-web-service
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "exceptions [Reporting Services], best practices"
---
# Best Practices for Reporting Services Exception Handling
  When developing [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] applications, there are several methodologies you can use to eliminate or reduce the occurrence of exceptions. When exceptions do occur, provide clear and concise error messages to the user, and add adequate exception handling to prevent your applications from ending unexpectedly.  
  
 An application that sends requests to the Report Server Web service should do the following:  
  
-   Avoid causing exceptions by preventing as many invalid requests as possible.  
  
-   Catch exceptions and provide specific error-handling code whenever possible.  
  
-   Deal with error cases that do not throw exceptions.  
  
## In This Section  
  
|Topic|Description|  
|-----------|-----------------|  
|[Preventing Invalid Requests](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|Describes techniques for preventing requests that are not valid from being sent to the report server.|  
|[Using Try and Catch Blocks](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|Describes how to further enhance the reliability of your application with try/catch blocks.|  
|[Handling Warnings and Cases That Do Not Cause Exceptions](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|Explains how to handle errors that do not result in an exception being thrown by [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Using the Detail Property to Handle Specific Errors](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|Explains how to programmatically handle specific errors by using the **Detail** property of the **SoapException** object.|  
  
## See Also  
 [Detail Property](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Introducing Exception Handling in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException Class](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
