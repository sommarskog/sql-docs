---
title: "Creating the Server Connection Files (DB2ToSQL)"
description: "Creating the Server Connection Files (DB2ToSQL)"
author: cpichuka
ms.author: cpichuka
ms.date: "07/14/2020"
ms.service: sql
ms.subservice: ssma
ms.topic: conceptual
---

# Creating the Server Connection Files (DB2ToSQL)

Server information can be specified either in the servers section of the script file or in a separate server connection file. The command line parameter for the server connection file is, `-c <serverconnectionfile>`. If the same server ID is present in both the script file and server connection file, then the server definition in the script file is considered.

**Example: 1**

```xml
<!-- Sample of server connection file commands -->
<db2 name="<source-server-unique-name>">
  <standard-mode>

    <connection-provider value="OleDB Provider" />

    <!-- Defines server manager to connect.
         Available manager attribute values
           • zOs - DB2 for z/OS
           • LUW - DB2 for Linux, Unix and Windows
           • DBi - DB2 for i -->
    <database-manager value="$Db2Manager$" />

    <server-name value="$Db2HostName$" />

    <port value="$Db2Port$" />

    <initial-catalog value="$Db2Instance$" />

    <user-id value="$Db2UserName$" />

    <password value="$Db2Password$"/>

  </standard-mode>
</db2>
```

```xml
<sql-server name="<target-server-unique-name>">
  <sql-server-authentication>

    <server value="<server-name>" />

    <database value="<database-name>" />
  
    <user-id value="<user-name>"/>
  
    <password value="<password>"/>

  </sql-server-authentication>
</sql-server>
```

## Next Step

The next step in operating the console is [Executing the SSMA Console &#40;DB2ToSQL&#41;](../../ssma/db2/executing-the-ssma-console-db2tosql.md)

## See Also

- [Executing the SSMA Console](./executing-the-ssma-console-db2tosql.md)
