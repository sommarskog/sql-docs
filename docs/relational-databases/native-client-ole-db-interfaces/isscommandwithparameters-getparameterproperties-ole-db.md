---
title: "ISSCommandWithParameters::GetParameterProperties (OLE DB)"
description: "ISSCommandWithParameters::GetParameterProperties in SQL Server Native Client (OLE DB)"
author: markingmyname
ms.author: maghan
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: native-client
ms.topic: "reference"
helpviewer_keywords:
  - "GetParameterProperties method"
apiname: "ISSCommandWithParameters::GetParameterProperties (OLE DB)"
apitype: "COM"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# ISSCommandWithParameters::GetParameterProperties in SQL Server Native Client (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

> [!IMPORTANT]
> [!INCLUDE[snac-removed-oledb-only](../../includes/snac-removed-oledb-only.md)]

  Returns an array of SSPARAMPROPS property set structures, one SSPARAMPROPS property set for each UDT or XML parameter.  
  
## Syntax  
  
```cpp
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## Arguments  
 *pcParams*[out][in]  
 A pointer to memory that contains the number of SSPARAMPROPS structures returned in *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 A pointer to memory in which an array of SSPARAMPROPS structures is returned. The provider allocates memory for the structures and returns the address to this memory; the consumer releases this memory with **IMalloc::Free** when it no longer needs the structures. Before calling **IMalloc::Free** for *prgParamProperties*, the consumer must also call **VariantClear** for the *vValue* property of each DBPROP structure in order to prevent a memory leak in cases where the variant contains a reference type (such as a BSTR.) If *pcParams* is zero on output or an error other than DB_E_ERRORSOCCURRED occurs, the provider does not allocate any memory and ensures that *prgParamProperties* is a null pointer on output.  
  
## Return Code Values  
 The **GetParameterProperties** method returns the same error codes as the core OLE DB **ICommandProperties::GetProperties** method, except that DB_S_ERRORSOCCURRED and DB_E_ERRORSOCCURED cannot be raised.  
  
## Remarks  
 **ISSCommandWithParameters::GetParameterProperties** behaves consistently with respect to **GetParameterInfo**. If [ISSCommandWithParameters::SetParameterProperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) or **SetParameterInfo** have not been called or have been called with cParams equal to zero, **GetParameterInfo** derives parameter information and returns this. If **ISSCommandWithParameters::SetParameterProperties** or **SetParameterInfo** have been called for at least one parameter, **ISSCommandWithParameters::GetParameterProperties** returns properties only for those parameters for which **ISSCommandWithParameters::SetParameterProperties** has been called. If **ISSCommandWithParameters::SetParameterProperties** is called after **ISSCommandWithParameters::GetParameterProperties** or **GetParameterInfo**, subsequent calls to **ISSCommandWithParameters::GetParameterProperties** return the overridden values for those parameters for which **ISSCommandWithParameters::SetParameterProperties** has been called.  
  
 The SSPARAMPROPS structure is defined as follows:  

```cpp
struct SSPARAMPROPS {
    DBORDINAL iOrdinal;
    ULONG cPropertySets;
    DBPROPSET *rgPropertySets;
};
```

|Member|Description|  
|------------|-----------------|  
|*iOrdinal*|The ordinal of the passed parameter.|  
|*cPropertySets*|The number of DBPROPSET structures in *rgPropertySets*.|  
|*rgPropertySets*|A pointer to memory in which to return an array of DBPROPSET structures.|  

## See Also  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
