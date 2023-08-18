---
title: "Determine effective Database Engine permissions"
description: Learn how to determine who has permissions to various objects in the SQL Server Database Engine, including the current and previous permissions systems.
author: VanMSFT
ms.author: vanto
ms.reviewer: randolphwest
ms.date: 10/14/2022
ms.service: sql
ms.subservice: security
ms.topic: conceptual
helpviewer_keywords:
  - "permissions, effective"
  - "effective permissions"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Determine effective Database Engine permissions

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

This article describes how to determine who has permissions to various objects in the [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] [!INCLUDE [ssde-md](../../../includes/ssde-md.md)]. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] implements two permission systems for the [!INCLUDE [ssde-md](../../../includes/ssde-md.md)]. An older system of fixed roles has preconfigured permissions. Beginning with [!INCLUDE [ssversion2005-md](../../../includes/ssversion2005-md.md)] a more flexible and precise system is available.

> [!NOTE]  
> The information in this article applies to [!INCLUDE [ssversion2005-md](../../../includes/ssversion2005-md.md)] and later versions. Some types of permissions are not available in some versions of [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

You should always keep the following points in mind:

- The effective permissions are the aggregate of both permission systems.
- A denial of permissions overrides a grant of permissions.
- If a user is a member of the sysadmin fixed server role, permissions aren't checked further, so denials won't be enforced.
- The old system and new system have similarities. For example, membership in the `sysadmin` fixed server role is similar to having `CONTROL SERVER` permission. But the systems aren't identical. For example, if a login only has the `CONTROL SERVER` permission, and a stored procedures check for membership in the `sysadmin` fixed server role, then the permission check will fail. The reverse is also true.

## Summary

- Server-level permission can come from membership in the fixed server roles or user-defined server roles. Everyone belongs to the `public` fixed server role and receives any permission assigned there.
- Server-level permissions can come from permission grants to logins or user-defined server roles.
- Database-level permission can come from membership in the fixed database roles or user-defined database roles in each database. Everyone belongs to the `public` fixed database role and receives any permission assigned there.
- Database-level permissions can come from permission grants to users or user-defined database roles in each database.
- Permissions can be received from the `guest` login or `guest` database user if enabled. The `guest` login and users are disabled by default.
- Windows users can be members of Windows groups that can have logins. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] learns of Windows group membership when a Windows user connects and presents a Windows token with the security identifier of a Windows group. Because [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] doesn't manage or receive automatic updates about Windows group memberships, [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] can't reliably report the permissions of Windows users that are received from Windows group membership.
- Permissions can be acquired by switching to an application role and providing the password.
- Permissions can be acquired by executing a stored procedure that includes the `EXECUTE AS` clause.
- Permissions can be acquired by logins or users with the `IMPERSONATE` permission.
- Members of the local computer administrator group can always elevate their privileges to `sysadmin`. (Doesn't apply to SQL Database.)
- Members of the `securityadmin` fixed server role can elevate many of their privileges and in some cases can elevate the privileges to `sysadmin`. (Doesn't apply to SQL Database.)
- [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] administrators can see information about all logins and users. Less privileged users usually see information about only their own identities.

## Older fixed role permission system

Fixed server roles and fixed database roles have preconfigured permissions that can't be changed. To determine who is a member of a fixed server role, execute the following query:

> [!NOTE]  
> Does not apply to SQL Database or Azure Synapse Analytics where server level permission is not available. The `is_fixed_role` column of `sys.server_principals` was added in [!INCLUDE [sssql11-md](../../../includes/sssql11-md.md)]. It is not needed for older versions of [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

```sql
SELECT SP1.name AS ServerRoleName,
    ISNULL(SP2.name, 'No members') AS LoginName
FROM sys.server_role_members AS SRM
RIGHT JOIN sys.server_principals AS SP1
    ON SRM.role_principal_id = SP1.principal_id
LEFT JOIN sys.server_principals AS SP2
    ON SRM.member_principal_id = SP2.principal_id
WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
ORDER BY SP1.name;
```

> [!NOTE]  
> All logins are members of the public role and cannot be removed. The query checks tables in the `master` database, but it can be executed in any database for the on-premises product.

To determine who is a member of a fixed database role, execute the following query in each database.

```sql
SELECT DP1.name AS DatabaseRoleName,
    ISNULL(DP2.name, 'No members') AS DatabaseUserName
FROM sys.database_role_members AS DRM
RIGHT JOIN sys.database_principals AS DP1
    ON DRM.role_principal_id = DP1.principal_id
LEFT JOIN sys.database_principals AS DP2
    ON DRM.member_principal_id = DP2.principal_id
WHERE DP1.is_fixed_role = 1
ORDER BY DP1.name;
```

To understand the permissions that are granted to each role, see the role descriptions at illustrations in Books Online ([Server-level roles](../../../relational-databases/security/authentication-access/server-level-roles.md), and [Database-level roles](../../../relational-databases/security/authentication-access/database-level-roles.md)).

## Newer granular permission system

This system is flexible, which means it can be complicated if the people setting it up want to be precise. To simplify matters it helps to create roles, assign permissions to roles, and then add groups of people to the roles. And it's easier if the database development team separates activity by schema and then grants role permissions to a whole schema instead of to individual tables or procedures. Real world scenarios are complex and business needs can create unexpected security requirements.

[!INCLUDE[database-engine-permissions](../../includes/database-engine-permissions.md)]

### Security classes

Permissions can be granted at the server-level, the database-level, the schema-level, or the object-level, etc. There are 26 levels (called classes). The complete list of classes in alphabetic order is: `APPLICATION ROLE`, `ASSEMBLY`, `ASYMMETRIC KEY`, `AVAILABILITY GROUP`, `CERTIFICATE`, `CONTRACT`, `DATABASE`, `DATABASE` `SCOPED CREDENTIAL`, `ENDPOINT`, `FULLTEXT CATALOG`, `FULLTEXT STOPLIST`, `LOGIN`, `MESSAGE TYPE`, `OBJECT`, `REMOTE SERVICE BINDING`, `ROLE`, `ROUTE`, `SCHEMA`, `SEARCH PROPERTY LIST`, `SERVER`, `SERVER ROLE`, `SERVICE`, `SYMMETRIC KEY`, `TYPE`, `USER`, `XML SCHEMA COLLECTION`. (Some classes aren't available on some types of [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].) To provide full information about each class requires a different query.

### Principals

Permissions are granted to *principals*. Principals can be server roles, logins, database roles, or users. Logins can represent Windows groups that include many Windows users. Since Windows groups aren't maintained by [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] doesn't always know who is a member of a Windows group. When a Windows user connects to [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], the login packet contains the Windows group membership tokens for the user.

When a Windows user connects using a login based on a Windows group, some activities may require [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] to create a login or user to represent the individual Windows user. For example, a Windows group (Engineers) contains users (Mary, Todd, Pat) and the Engineers group has a database user account. If Mary has permission and creates a table, a user (Mary) might be created to be the owner of the table. Or if Todd is denied a permission that the rest of the Engineers group has, then the user Todd must be created to track the permission denial.

Remember that a Windows user might be a member of more than one Windows group (for example, both Engineers and Managers). Permissions granted or denied to the Engineers login, to the Managers login, granted or denied to the user individually, and granted or denied to roles that the user is a member of, will all be aggregated and evaluated to for the effective permissions. The `HAS_PERMS_BY_NAME` function can reveal whether a user or login has a particular permission. However, there is no obvious way of determining the source of the grant or denial of permission. Study the list of permissions and perhaps experiment using trial and error.

## Useful queries

### Server permissions

The following query returns a list of the permissions that have been granted or denied at the server level. This query should be executed in the `master` database.

> [!NOTE]  
> Server-level permissions cannot be granted or queried on SQL Database or Azure Synapse Analytics.

```sql
SELECT pr.type_desc,
    pr.name,
    ISNULL(pe.state_desc, 'No permission statements') AS state_desc,
    ISNULL(pe.permission_name, 'No permission statements') AS permission_name
FROM sys.server_principals AS pr
LEFT JOIN sys.server_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
ORDER BY pr.name,
    type_desc;
```

### Database permissions

The following query returns a list of the permissions that have been granted or denied at the database level. This query should be executed in each database.

```sql
SELECT pr.type_desc,
    pr.name,
    ISNULL(pe.state_desc, 'No permission statements') AS state_desc,
    ISNULL(pe.permission_name, 'No permission statements') AS permission_name
FROM sys.database_principals AS pr
LEFT JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0
ORDER BY pr.name,
    type_desc;
```

Each class of permission the permission table can be joined to other system views that provide related information about that class of securable. For example, the following query provides the name of the database object that is affected by the permission.

```sql
SELECT pr.type_desc,
    pr.name,
    pe.state_desc,
    pe.permission_name,
    s.name + '.' + oj.name AS OBJECT,
    major_id
FROM sys.database_principals AS pr
INNER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
INNER JOIN sys.objects AS oj
    ON oj.object_id = pe.major_id
INNER JOIN sys.schemas AS s
    ON oj.schema_id = s.schema_id
WHERE class_desc = 'OBJECT_OR_COLUMN';
```

Use the `HAS_PERMS_BY_NAME` function to determine if a particular user (in this case `TestUser`) has a permission. For example:

```sql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```

For the details of the syntax, see [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md).

## Next steps

- [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)
- [Tutorial: Getting Started with Database Engine](../../../relational-databases/tutorial-getting-started-with-the-database-engine.md)
