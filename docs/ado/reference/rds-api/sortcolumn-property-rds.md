---
title: "SortColumn Property (RDS)"
description: "SortColumn Property (RDS)"
author: rothja
ms.author: jroth
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ado
ms.topic: reference
helpviewer_keywords:
  - "SortColumn property [RDS]"
apitype: "COM"
---
# SortColumn Property (RDS)
Indicates by which column to sort the records.  
  
> [!IMPORTANT]
>  Beginning with Windows 8 and Windows Server 2012, RDS server components are no longer included in the Windows operating system (see Windows 8 and [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) for more detail). RDS client components will be removed in a future version of Windows. Avoid using this feature in new development work, and plan to modify applications that currently use this feature. Applications that use RDS should migrate to [WCF Data Service](/dotnet/framework/wcf/).  
  
## Syntax  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### Parameters  
 *DataControl*  
 An object variable that represents an [RDS.DataControl](./datacontrol-object-rds.md) object.  
  
 *String*  
 A **String** value that represents the name or alias of the column by which to sort the records.  
  
## Remarks  
 The **SortColumn**, [SortDirection](./sortdirection-property-rds.md), [FilterValue](./filtervalue-property-rds.md), [FilterCriterion](./filtercriterion-property-rds.md), and [FilterColumn](./filtercolumn-property-rds.md) properties provide sorting and filtering functionality on the client-side cache. The sorting functionality orders records by values from one column. The filtering functionality displays a subset of records based on find criteria, while the full [Recordset](../ado-api/recordset-object-ado.md) is maintained in the cache. The [Reset](./reset-method-rds.md) method will execute the criteria and replace the current **Recordset** with an updatable **Recordset**.  
  
 To sort on a **Recordset**, you must first save any pending changes. If you are using the **RDS.DataControl**, you can use the [SubmitChanges](./submitchanges-method-rds.md) method. For example, if your **RDS.DataControl** is named ADC1, your code would be `ADC1.SubmitChanges`. If you are using an ADO **Recordset**, you can use its [UpdateBatch](../ado-api/updatebatch-method.md) method. Using **UpdateBatch** is the recommended method for **Recordset** objects created with the [CreateRecordset](./createrecordset-method-rds.md) method. For example, your code could be `myRS.UpdateBatch` or `ADC1.Recordset.UpdateBatch`.  
  
## Applies To  
 [DataControl Object (RDS)](./datacontrol-object-rds.md)  
  
## See Also  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, and SortDirection Properties and Reset Method Example (VBScript)](./filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Sort Property](../ado-api/sort-property.md)   
 [SortDirection Property (RDS)](./sortdirection-property-rds.md)