---
title: "IBCPSession::BCPExec (OLE DB driver)"
description: "The IBCPSession::BCPExec method copies data from a user file to a database table or vice versa in OLE DB Driver for SQL Server."
author: David-Engel
ms.author: v-davidengel
ms.date: "06/14/2018"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "BCPExec method"
apiname: "IBCPSession::BCPExec (OLE DB)"
apitype: "COM"
---
# IBCPSession::BCPExec (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Performs the bulk copy operation.  
  
## Syntax  
  
```  
  
HRESULT BCPExec(   
      DBROWCOUNT *pRowsCopied);  
```  
  
## Remarks  
 The **BCPExec** method copies data from a user file to a database table or vice versa, depending on the value of the *eDirection* parameter used with the [IBCPSession::BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md) method.  
  
 Before calling **BCPExec**, call the **BCPInit** method with a valid user file name. Failure to do so results in an error. The only exception is if a query is to be used for a bulk copy out operation. In that case specify NULL for the table name in the **BCPInit** method and then specify the query using the BCP_OPTION_HINTS option.  
  
 The **BCPExec** method is the only bulk copy method that is likely to be outstanding for any length of time. It is therefore the only bulk copy method that supports asynchronous mode. To use asynchronous mode, set the provider specific session property SSPROP_ASYNCH_BULKCOPY to VARIANT_TRUE before calling the **BCPExec** method. This property is available in the DBPROPSET_SQLSERVERSESSION property set. To test for completion, call the **BCPExec** method with the same parameters. If the bulk copy has not yet completed, the **BCPExec** method returns DB_S_ASYNCHRONOUS. It also returns in the *pRowsCopied* argument a status count of the number of rows that have been sent to or received from the server. Rows sent to the server are not committed until the end of a batch has been reached.  
  
## Arguments  
 *pRowsCopied*[out]  
 A pointer to a DWORD. The **BCPExec** method fills the DWORD with the number of rows successfully copied. If the *pRowsCopied* argument is set to NULL, it is ignored by the **BCPExec** method.  
  
## Return Code Values  
 S_OK  
 The method succeeded.  
  
 E_FAIL  
 A provider-specific error occurred; for detailed information, use the [ISQLServerErrorInfo](./isqlservererrorinfo-geterrorinfo-ole-db.md) interface.  
  
 E_UNEXPECTED  
 The call to the method was unexpected. For example, the **BCPInit** method was not called before calling this method. Also occurs if the operation has been aborted through using the BCP_OPTION_ABORT option, and the **BCPExec** method was called afterwards.  
  
 E_OUTOFMEMORY  
 Out-of-memory error.  
  
 DB_S_ENDOFROWSET  
 The bulk copy operation finished, and all the data transfer was completed.  
  
 DB_S_ASYNCHRONOUS  
 The current batch of rows has been copied. Call the **BCPExec** method again to transfer the next batch.  
  
 DB_S_ERRORSOCCURRED  
 Errors occurred during the bulk copy operation, and some rows might not have been copied. The number of errors is still less than the maximum errors allowed.  
  
## See Also  
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Performing Bulk Copy Operations](../../oledb/features/performing-bulk-copy-operations.md)  
  
