---
title: "Accessing Rows in a Hierarchical Recordset"
description: "Accessing Rows in a Hierarchical Recordset (Example)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: conceptual
helpviewer_keywords:
  - "hierarchical Recordsets [ADO]"
  - "data shaping [ADO], hierarchical Recordsets"
---
# Accessing Rows in a Hierarchical Recordset (Example)
The following example shows the steps necessary to access rows in a hierarchical [Recordset](../../reference/ado-api/recordset-object-ado.md):

1.  **Recordset** objects from the **authors** and **titleauthor** tables are related by author ID.

2.  The outer loop displays each author's first and last name, state, and identification.

3.  The appended **Recordset** for each row is retrieved from the [Fields](../../reference/ado-api/fields-collection-ado.md) collection and assigned to *rstTitleAuthor*.

4.  The inner loop displays four fields from each row in the appended **Recordset**.

 The [StayInSync](../../reference/ado-api/stayinsync-property.md) property is set to **false** for purposes of illustration, so that you can see the chapter change explicitly in each iteration of the outer loop. To make the code example more efficient, you can move the assignment in step 3 before the first line in step 2, so that the assignment is performed only once. Then set the [StayInSync](../../reference/ado-api/stayinsync-property.md) property to **true**, so that *rstTitleAuthor* will implicitly and automatically change to the corresponding chapter whenever *rst* moves to a new row.

## Example

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## See Also
 [Data Shaping Overview](./data-shaping-overview.md)
 [Field Object](../../reference/ado-api/field-object.md)
 [Fields Collection (ADO)](../../reference/ado-api/fields-collection-ado.md)
 [Formal Shape Grammar](./formal-shape-grammar.md)
 [Microsoft Data Shaping Service for OLE DB (ADO Service Provider)](../appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
 [Recordset Object (ADO)](../../reference/ado-api/recordset-object-ado.md)
 [Required Providers for Data Shaping](./required-providers-for-data-shaping.md)
 [Shape APPEND Clause](./shape-append-clause.md)
 [Shape Commands in General](./shape-commands-in-general.md)
 [Shape COMPUTE Clause](./shape-compute-clause.md)
 [Visual Basic for Applications functions](./visual-basic-for-applications-functions.md)