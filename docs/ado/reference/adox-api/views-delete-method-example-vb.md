---
title: "Views Delete Method Example (VB)"
description: "Views Delete Method Example (VB)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
helpviewer_keywords:
  - "Delete method [ADOX]"
dev_langs:
  - "VB"
---
# Views Delete Method Example (VB)
The following code shows how to use the [Delete](./delete-method-adox-collections.md) method to delete a view from the catalog.  
  
```  
' BeginDeleteViewVB  
Sub Main()  
    On Error GoTo DeleteViewError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    'Delete the View  
    cat.Views.Delete "AllCustomers"  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteViewError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteViewVB  
```  
  
## See Also  
 [Delete Method (ADOX Collections)](./delete-method-adox-collections.md)   
 [Views Collection (ADOX)](./views-collection-adox.md)