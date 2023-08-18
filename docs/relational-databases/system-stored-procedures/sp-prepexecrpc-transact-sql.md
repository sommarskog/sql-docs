---
title: "sp_prepexecrpc (Transact-SQL)"
description: "sp_prepexecrpc (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "06/02/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_cursor_prepexecrpc"
  - "sp_cursor_prepexecrpc_TSQL"
helpviewer_keywords:
  - "sp_prepexecrpc"
dev_langs:
  - "TSQL"
---
# sp_prepexecrpc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Prepares and executes a parameterized stored procedure call that has been specified using an RPC identifier. sp_prepexecrpc is invoked by ID = 14 in a tabular data stream (TDS) packet.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## Arguments  
 *handle*  
 Is the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-generated prepared handle identifier. *handle* is a required parameter with an **int** return value.  
  
 *RPCCall*  
 Defines the stored procedure call using ODBC canonical syntax. *RPCCall* is a required parameter that calls for an **ntext** string input value.  
  
 *bound_param*  
 Signifies the optional use of additional parameters. *bound_param* calls for an input value of any data type to designate the additional parameters in use.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
