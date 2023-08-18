---
title: "Connect to Oracle (OracleToSQL)"
description: Learn how to connect to an Oracle database to begin migration using SSMA for Oracle. Use the Connect to Oracle dialog box.
author: cpichuka
ms.author: cpichuka
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
---

# Connect to Oracle (OracleToSQL)

Use the **Connect to Oracle** dialog box to connect to the Oracle database that you want to migrate.

To access this dialog box, on the **File** menu, select **Connect to Oracle**. If you have previously connected, the command is **Reconnect to Oracle**.

## Options

**Provider**  
Select the data access provider for your connection to the Oracle database. Available providers are the Oracle Client Provider and the OLE DB Provider. The default is Oracle Client Provider.

**Mode**  
Select either Standard, TNSNAME, or Connection String mode.

- In Standard mode, you enter or select values for the provider, server name, server port, Oracle SID, user name, and password.
- In TNSNAME mode, you enter the connect identifier (TNS alias) of the Oracle database, user name, and password.
- In Connection String mode, you provide a connection string.

  > [!IMPORTANT]
  > We do not recommend that you use Connection String mode because the text might include passwords, and it is sent as clear text.

The default is Standard mode.

**Server name**  
Enter the Oracle server name. The default server name is the same as the computer name. This is a Standard mode option.

**Server port**  
If you are using a port number other than 1521 (default) for connections to Oracle, enter the port number. This is a Standard mode option.

**Connect identifier**  
Enter the Oracle connect identifier. This is the alias of the database as defined in local tnsnames.ora file.

This is a TNSNAME mode option.

**Oracle SID**  
Enter the SID for the database. The SID is an identifier that distinguishes the Oracle database on a computer. The default SID for a database is the first eight characters of the database name.

This is a Standard mode option.

**User name**  
Enter the user name that SSMA will use to connect to the Oracle database.

**Password**  
Enter the password for the user name.

**Connection string**  
> [!IMPORTANT]
> We do not recommend that you use Connection String mode because the text might include passwords, and it is sent as clear text.

If you use the Connection String mode, enter the full connection string for the connection to Oracle.

Connection strings consist of parameter name and value pairs.

- For OLE DB connection string information, see [Microsoft OLE DB Provider for Oracle](../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) article at the MSDN Library.

For SSMA connection strings, always include the Provider parameter. Also, make sure that you include the Port parameter when you connect to Oracle.

## Next steps

The next step in the migration process is to [Connect to SQL Server](connect-to-sql-server-oracletosql.md).
