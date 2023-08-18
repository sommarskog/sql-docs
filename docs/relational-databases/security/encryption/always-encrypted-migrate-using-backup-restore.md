---
title: "Backup and restore databases using Always Encrypted"
description: "Backup and restore databases using Always Encrypted"
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
ms.date: 10/30/2019
ms.service: sql
ms.subservice: security
ms.topic: conceptual
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Backup and restore databases using Always Encrypted 
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../../includes/applies-to-version/sql-asdb-asdbmi.md)]

This article describes how to back up and restore a database containing columns protected with [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md).

When you back up a database, the resulting backup file contains encrypted stored in encrypted columns and all metadata for Always Encrypted keys.

When you restore a database, all encrypted data and all metadata for Always Encrypted keys are restored. 

If you restored the database on a different server or under a different name, you don't need to do anything special to enable the application to query the encrypted data in the target database, as the keys in both databases are the same.

For detailed information about how to back up and restore a database, see:
- [Backup Overview (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [Restore a database to Azure SQL Managed Instance with SSMS](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)

## Next steps
- [Query columns using Always Encrypted with SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Develop applications using Always Encrypted with secure enclaves](always-encrypted-enclaves-client-development.md) 

## See also
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Export and import databases using Always Encrypted](always-encrypted-migrate-using-bacpac.md)
- [Migrate data to or from columns using Always Encrypted with SQL Server Import and Export Wizard](always-encrypted-migrate-using-import-export-wizard.md)
- [Bulk load encrypted data to columns using Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)
