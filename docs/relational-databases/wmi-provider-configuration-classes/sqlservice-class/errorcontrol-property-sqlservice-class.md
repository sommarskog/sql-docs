---
title: "ErrorControl Property (SqlService)"
description: "ErrorControl Property (SqlService Class)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "ErrorControl property"
apilocation: "sqlmgmproviderxpsp2up.mof"
apiname: "ErrorControl Property (SqlService Class)"
apitype: "MOFDef"
---
# ErrorControl Property (SqlService Class)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Gets or sets the severity of the error if the service fails to start during startup.  
  
## Syntax  
  
```  
  
object.ErrorControl [= value]  
```  
  
## Parts  
 *object*  
 A [SqlService Class](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) object that represents the service.  
  
## Property Value/Return Value  
 A string value that specifies the error severity reported if the service fails during startup. The following table shows the possible values.  
  
 Ignore  
 User is not notified.  
  
 Normal  
 User is notified.  
  
 Severe  
 System is restarted with the last-known-good configuration.  
  
 Critical  
 System attempts to restart with a good configuration.  
  
 Unknown  
 The severity is unknown.  
  
## Remarks  
 The value indicates the action taken by the startup program if a failure occurs. All errors are logged by the computer system.  
  
## See Also  
 [Starting and Stopping Services](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
