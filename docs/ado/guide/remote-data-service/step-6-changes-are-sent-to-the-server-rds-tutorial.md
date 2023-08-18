---
title: "Step 6: Changes are Sent to the Server (RDS Tutorial)"
description: "Step 6: Changes are Sent to the Server (RDS Tutorial)"
author: rothja
ms.author: jroth
ms.date: 11/09/2018
ms.service: sql
ms.subservice: ado
ms.topic: conceptual
helpviewer_keywords:
  - "RDS tutorial [ADO], changes sent to server"
---
# Step 6: Changes are Sent to the Server (RDS Tutorial)
If the **Recordset** object is edited, any changes (that is, rows that are added, changed, or deleted) can be sent back to the server.  
  
> [!NOTE]
>  The default behavior of RDS can be invoked implicitly with ADO objects and the Microsoft OLE DB Remoting Provider. Queries can return **Recordset**s, and edited **Recordset**s can update the data source. This tutorial does not invoke RDS with ADO objects, but this is how it would look if it did:  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **Part A** Assume for this case that you have only used the [RDS.DataControl](../../reference/rds-api/datacontrol-object-rds.md) and that a **Recordset** object is now associated with the **RDS.DataControl**. The [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md) method updates the data source with any changes to the **Recordset** object if the [Server](../../reference/rds-api/server-property-rds.md) and [Connect](../../reference/rds-api/connect-property-rds.md) properties are still set.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **Part B** Alternatively, you could update the server with the [RDSServer.DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) object, specifying a connection and a **Recordset** object.  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **This is the end of the tutorial.**  
  
> [!IMPORTANT]
>  Beginning with Windows 8 and Windows Server 2012, RDS server components are no longer included in the Windows operating system (see Windows 8 and [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) for more detail). RDS client components will be removed in a future version of Windows. Avoid using this feature in new development work, and plan to modify applications that currently use this feature. Applications that use RDS should migrate to [WCF Data Service](/dotnet/framework/wcf/).  
  
## See Also  
 [Microsoft OLE DB Remoting Provider (ADO Service Provider)](../appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS Tutorial](./rds-tutorial.md)   
 [RDS Tutorial (VBScript)](./rds-tutorial-vbscript.md)