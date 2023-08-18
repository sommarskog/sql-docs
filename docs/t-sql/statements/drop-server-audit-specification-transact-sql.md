---
title: "DROP SERVER AUDIT SPECIFICATION (Transact-SQL)"
description: DROP SERVER AUDIT SPECIFICATION (Transact-SQL)
author: sravanisaluru
ms.author: srsaluru
ms.date: "03/23/2022"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "DROP_SERVER_AUDIT_SPECIFICATION_TSQL"
  - "DROP SERVER AUDIT SPECIFICATION"
helpviewer_keywords:
  - "server audit [SQL Server]"
  - "audits [SQL Server], specification"
  - "DROP SERVER AUDIT SPECIFICATION statement"
dev_langs:
  - "TSQL"
---
# DROP SERVER AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Drops a server audit specification object using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit feature. For more information, see [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql 
DROP SERVER AUDIT SPECIFICATION audit_specification_name  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *audit_specification_name*  
 Name of an existing server audit specification object.  
  
## Remarks  
 A DROP SERVER AUDIT SPECIFICATION removes the metadata for the audit specification, but not the audit data collected before the DROP command was issued. You must set the state of a server audit specification to OFF using ALTER SERVER AUDIT SPECIFICATION before it can be dropped.  
  
## Permissions  
 Users with the ALTER ANY SERVER AUDIT permission can drop server audit specifications.  
  
## Examples  
 The following example drops a server audit specification called `HIPAA_Audit_Specification`.  
  
```sql  
DROP SERVER AUDIT SPECIFICATION HIPAA_Audit_Specification;  
GO  
```  
  
 For a full example about how to create an audit, see [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## See Also  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Create a Server Audit and Server Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
