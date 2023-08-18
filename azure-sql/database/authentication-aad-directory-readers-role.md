---
title: Directory Readers role in Azure Active Directory for Azure SQL
description: Learn about the directory reader's role in Azure AD for Azure SQL.
author: nofield
ms.author: nofield
ms.reviewer: wiassaf, vanto, mathoma
ms.date: 12/15/2021
ms.service: sql-db-mi
ms.subservice: security
ms.topic: conceptual
ms.custom: azure-synapse
monikerRange: "= azuresql || = azuresql-db || = azuresql-mi"
---

# Directory Readers role in Azure Active Directory for Azure SQL

[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]

Azure Active Directory (Azure AD) has introduced [using Azure AD groups to manage role assignments](/azure/active-directory/roles/groups-concept). This allows for Azure AD roles to be assigned to groups.

> [!NOTE]
> With [Microsoft Graph](/graph/overview) support for Azure SQL, the Directory Readers role can be replaced with using lower level permissions. For more information, see [User-assigned managed identity in Azure AD for Azure SQL](authentication-azure-ad-user-assigned-managed-identity.md).

When enabling a [managed identity](/azure/active-directory/managed-identities-azure-resources/overview#managed-identity-types) for Azure SQL Database, Azure SQL Managed Instance, or Azure Synapse Analytics, the Azure AD [**Directory Readers**](/azure/active-directory/roles/permissions-reference#directory-readers) role can be assigned to the identity to allow read access to the [Microsoft Graph API](/graph/overview). The managed identity of SQL Database and Azure Synapse is referred to as the server identity. The managed identity of SQL Managed Instance is referred to as the managed instance identity, and is automatically assigned when the instance is created. For more information on assigning a server identity to SQL Database or Azure Synapse, see [Enable service principals to create Azure AD users](authentication-aad-service-principal.md#enable-service-principals-to-create-azure-ad-users).

The **Directory Readers** role can be used as the server or instance identity to help:

- Create Azure AD logins for SQL Managed Instance
- Impersonate Azure AD users in Azure SQL
- Migrate SQL Server users that use Windows authentication to SQL Managed Instance with Azure AD authentication (using the [ALTER USER (Transact-SQL)](/sql/t-sql/statements/alter-user-transact-sql?view=azuresqldb-mi-current&preserve-view=true#d-map-the-user-in-the-database-to-an-azure-ad-login-after-migration) command)
- Change the Azure AD admin for SQL Managed Instance
- Allow [service principals (Applications)](authentication-aad-service-principal.md) to create Azure AD users in Azure SQL

## Assigning the Directory Readers role

In order to assign the [**Directory Readers**](/azure/active-directory/roles/permissions-reference#directory-readers) role to an identity, a user with [Global Administrator](/azure/active-directory/roles/permissions-reference#global-administrator) or [Privileged Role Administrator](/azure/active-directory/roles/permissions-reference#privileged-role-administrator) permissions is needed. Users who often manage or deploy SQL Database, SQL Managed Instance, or Azure Synapse may not have access to these highly privileged roles. This can often cause complications for users that create unplanned Azure SQL resources, or need help from highly privileged role members that are often inaccessible in large organizations.

For SQL Managed Instance, the **Directory Readers** role must be assigned to managed instance identity before you can [set up an Azure AD admin for the managed instance](authentication-aad-configure.md#provision-azure-ad-admin-sql-managed-instance). 

Assigning the **Directory Readers** role to the server identity isn't required for SQL Database or Azure Synapse when setting up an Azure AD admin for the logical server. However, to enable an Azure AD object creation in SQL Database or Azure Synapse on behalf of an Azure AD application, the **Directory Readers** role is required. If the role isn't assigned to the SQL logical server identity, creating Azure AD users in Azure SQL will fail. For more information, see [Azure Active Directory service principal with Azure SQL](authentication-aad-service-principal.md).

## Granting the Directory Readers role to an Azure AD group

You can now have a [Global Administrator](/azure/active-directory/roles/permissions-reference#global-administrator) or [Privileged Role Administrator](/azure/active-directory/roles/permissions-reference#privileged-role-administrator) create an Azure AD group and assign the [**Directory Readers**](/azure/active-directory/roles/permissions-reference#directory-readers) permission to the group. This will allow access to the Microsoft Graph API for members of this group. In addition, Azure AD users who are owners of this group are allowed to assign new members for this group, including identities of the Azure SQL logical servers.

This solution still requires a high privilege user (Global Administrator or Privileged Role Administrator) to create a group and assign users as a one time activity, but the Azure AD group owners will be able to assign additional members going forward. This eliminates the need to involve a high privilege user in the future to configure all SQL Databases, SQL Managed Instances, or Azure Synapse servers in their Azure AD tenant.

## Next steps

> [!div class="nextstepaction"]
> [Tutorial: Assign Directory Readers role to an Azure AD group and manage role assignments](authentication-aad-directory-readers-role-tutorial.md)
