---
title: "Step 1: Specify a Server Program (RDS Tutorial)"
description: "Step 1: Specify a Server Program (RDS Tutorial)"
author: rothja
ms.author: jroth
ms.date: 11/09/2018
ms.service: sql
ms.subservice: ado
ms.topic: conceptual
helpviewer_keywords:
  - "RDS tutorial [ADO], specifying server program"
---
# Step 1: Specify a Server Program (RDS Tutorial)
In the most general case, use the [RDS.DataSpace](../../reference/rds-api/dataspace-object-rds.md) object [CreateObject](../../reference/rds-api/createobject-method-rds.md) method to specify the default server program, [RDSServer.DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md), or your own custom server program (business object). A server program is instantiated on the server, and a reference to the server program, or *proxy*, is returned.  
  
 This tutorial uses the default server program:  
  
```vb
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  Beginning with Windows 8 and Windows Server 2012, RDS server components are no longer included in the Windows operating system (see Windows 8 and [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) for more detail). RDS client components will be removed in a future version of Windows. Avoid using this feature in new development work, and plan to modify applications that currently use this feature. Applications that use RDS should migrate to [WCF Data Service](/dotnet/framework/wcf/).  
  
## See Also  
 [Step 2: Invoke the Server Program (RDS Tutorial)](./step-2-invoke-the-server-program-rds-tutorial.md)   
 [RDS Tutorial (VBScript)](./rds-tutorial-vbscript.md)