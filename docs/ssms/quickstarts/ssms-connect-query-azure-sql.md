---
title: Connect and query an Azure SQL Database or an Azure SQL Managed Instance using SQL Server Management Studio (SSMS)
description: Connect to an Azure SQL Database or an Azure SQL Managed Instance in SSMS. Create and query an Azure SQL Database or an Azure SQL Managed Instance in SSMS running basic T-SQL queries.
author: erinstellato-ms
ms.author: erinstellato
ms.reviewer: mikeray, randolphwest
ms.date: 06/19/2023
ms.service: sql
ms.subservice: ssms
ms.topic: quickstart
ms.custom: intro-quickstart
---
# Quickstart: Connect and query an Azure SQL Database or an Azure SQL Managed Instance using SQL Server Management Studio (SSMS)

[!INCLUDE [asdb](../../includes/applies-to-version/asdb.md)]

Get started using SQL Server Management Studio (SSMS) to connect to your Azure SQL Database and run some Transact-SQL (T-SQL) commands.

The article demonstrates the following steps:

> [!div class="checklist"]
> - Connect to an Azure SQL database
> - Create a database
> - Create a table in your new database
> - Insert rows into your new table
> - Query the new table and view the results
> - Use the query window table to verify your connection properties

## Prerequisites

- [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md) installed.
- [Azure SQL Database](https://azure.microsoft.com/free/sql-database/search/?&ef_id=CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE:G:s&OCID=AID2100131_SEM_CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE:G:s&gclid=CjwKCAiA17P9BRB2EiwAMvwNyDTqtKIHvBKK_qCTAnj3san_fx4KFjrSR8c58InygXQX5m_G71ZoMhoCzSMQAvD_BwE) or [Azure SQL Managed Instance](https://azure.microsoft.com/services/azure-sql/sql-managed-instance/)

## Connect to an Azure SQL Database or Azure SQL Managed Instance

[!INCLUDE[ssms-connect-azure-ad](../../includes/ssms-connect-azure-ad.md)]

1. Start SQL Server Management Studio. The first time you run SSMS, the **Connect to Server** window opens. If it doesn't open, you can open it manually by selecting **Object Explorer** > **Connect** > **Database Engine**.

   :::image type="content" source="media/ssms-connect-query-azure-sql/connect-object-explorer.png" alt-text="Screenshot of the Connect link in Object Explorer":::

1. The **Connect to Server** dialog box appears. Enter the following information:

   | Setting | Suggested value | Details |
   | --- | --- | --- |
   | **Server type** | Database Engine | Select **Database Engine** (usually the default option). |
   | **Server name** | The fully qualified server name | Enter the name of your *Azure SQL Database* or *Azure SQL Managed Instance* name. |
   | **Authentication** | | |
   | | Azure Active Directory <sup>1</sup> | |
   | | - Universal with MFA | See [Using multi-factor Azure Active Directory authentication](/azure/azure-sql/database/authentication-mfa-ssms-overview). |
   | | - Password<br />- Integrated<br />- Service Principal | See [Azure Active Directory service principal with Azure SQL](/azure/azure-sql/database/authentication-aad-service-principal). |
   | | - Managed Identity | See [Managed identities in Azure AD for Azure SQL](/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity).<br />Connecting to a SQL instance with SSMS using a managed identity requires an Azure VM. See [Use a Windows VM system-assigned managed identity to access Azure SQL](/azure/active-directory/managed-identities-azure-resources/tutorial-windows-vm-access-sql)  |
   | | - Default | The default option can be used when connecting using any Azure AD authentication mode that's passwordless and noninteractive. |
   | | SQL Server Authentication | Use **SQL Server Authentication** for Azure SQL to connect. |
   | **Login** | Server account user ID | The user ID from the server account used to create the server. |
   | **Password** | Server account password | The password from the server account used to create the server. |

   <sup>1</sup> The Windows Authentication method isn't supported for Azure SQL. For more information, see [Azure SQL authentication](/azure/sql-database/sql-database-security-overview#access-management).

   You can also modify additional connection options by selecting **Options**. Examples of connection options are the database you're connecting to, the connection timeout value, and the network protocol. This article uses the default values for all the options.

   :::image type="content" source="media/ssms-connect-query-azure-sql/connect-to-azure-sql-object-explorer.png" alt-text="Screenshot of Server name field for Azure SQL":::

1. After you've completed all the fields, select **Connect**.

   You can also modify additional connection options by selecting **Options**. Examples of connection options are the database you're connecting to, the connection timeout value, and the network protocol. This article uses the default values for all the options.

   If you haven't set up your firewall settings, a prompt appears to configure the firewall. Once you sign in, fill in your Azure account login information and continue to set the firewall rule. Then select **OK**. This prompt is a one time action. Once you configure the firewall, the firewall prompt shouldn't appear.

   :::image type="content" source="media/ssms-connect-query-azure-sql/azure-sql-firewall-sign-in-3.png" alt-text="Screenshot of Azure SQL New Firewall Rule":::

1. To verify that your Azure SQL Database or Azure SQL Managed Instance connection succeeded, expand and explore the objects within **Object Explorer** where the server name, the SQL Server version, and the username are displayed. These objects are different depending on the server type.

   :::image type="content" source="media/ssms-connect-query-azure-sql/connect-azure-sql.png" alt-text="Screenshot of connecting to a SQL Azure DB":::

## Troubleshoot connectivity issues

You can experience connection problems with Azure Synapse Analytics. For more information on troubleshooting connection problems, visit [Troubleshooting connectivity issues](/azure/azure-sql/database/troubleshoot-common-errors-issues).

You can prevent, troubleshoot, diagnose, and mitigate connection and transient errors that you encounter when interacting with Azure SQL Database or Azure SQL Managed Instance. For more information, visit [Troubleshoot transient connection errors](/azure/azure-sql/database/troubleshoot-common-connectivity-issues).

## Create a database

Now let's create a database named TutorialDB by following the below steps:

1. Right-click your server instance in Object Explorer, and then select **New Query**:

   :::image type="content" source="media/ssms-connect-query-azure-sql/new-query.png" alt-text="Screenshot showing the New Query link":::

1. Paste the following T-SQL code snippet into the query window:

   ```sql
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB];
   GO

   ALTER DATABASE [TutorialDB]
   SET QUERY_STORE = ON;
   GO
   ```

1. Execute the query by selecting **Execute** or selecting F5 on your keyboard.

   :::image type="content" source="media/ssms-connect-query-azure-sql/execute.png" alt-text="Screenshot showing the Execute command.":::

   After the query is complete, the new TutorialDB database appears in the list of databases in Object Explorer. If it isn't displayed, right-click the **Databases** node, and then select **Refresh**.

## Create a table in the new database

In this section, you create a table in the newly created TutorialDB database. Because the query editor is still in the context of the `master` database, switch the connection context to the *TutorialDB* database by doing the following steps:

1. In the database drop-down list, select the database that you want, as shown here:

   :::image type="content" source="media/ssms-connect-query-azure-sql/change-db.png" alt-text="Screenshot showing how to Change database.":::

1. Paste the following T-SQL code snippet into the query window:

   ```sql
   USE [TutorialDB];
   GO

   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
       DROP TABLE dbo.Customers;
   GO

   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers (
       CustomerId INT NOT NULL PRIMARY KEY, -- primary key column
       Name NVARCHAR(50) NOT NULL,
       Location NVARCHAR(50) NOT NULL,
       Email NVARCHAR(50) NOT NULL
   );
   GO
   ```

1. Execute the query by selecting **Execute** or selecting F5 on your keyboard.

After the query is complete, the new Customers table is displayed in the list of tables in Object Explorer. If the table isn't displayed, right-click the **TutorialDB** > **Tables** node in Object Explorer, and then select **Refresh**.

:::image type="content" source="media/ssms-connect-query-azure-sql/new-table.png" alt-text="Screenshot showing New table":::

## Insert rows into the new table

Now let's insert some rows into the Customers table that you created. Paste the following T-SQL code snippet into the query window, and then select **Execute**:

```sql
-- Insert rows into table 'Customers'
INSERT INTO dbo.Customers (
    [CustomerId],
    [Name],
    [Location],
    [Email]
)
VALUES
   (1, N'Orlando', N'Australia', N''),
   (2, N'Keith', N'India', N'keith0@adventure-works.com'),
   (3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
   (4, N'Janet', N'United States', N'janet1@adventure-works.com');
GO
```

## Query the table and view the results

The results of a query are visible below the query text window. To query the Customers table and view the rows that were inserted, follow these steps:

1. Paste the following T-SQL code snippet into the query window, and then select **Execute**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

   The results of the query are displayed under the area where the text was entered.

   :::image type="content" source="media/ssms-connect-query-azure-sql/query-results.png" alt-text="Screenshot showing the Results list.":::

   You can also modify the way results are presented by selecting one of the following options:

   :::image type="content" source="media/ssms-connect-query-azure-sql/results.png" alt-text="Screenshot of three options for displaying query results.":::

   - The first button displays the results in **Text View**, as shown in the image in the next section.
   - The middle button displays the results in **Grid View**, which is the default option.
     - This is set as default
   - The third button lets you save the results to a file whose extension is .rpt by default.

## Verify your connection properties by using the query window table

You can find information about the connection properties under the results of your query. After you run the previously mentioned query in the preceding step, review the connection properties at the bottom of the query window.

- You can determine which server and database you're connected to, and the username that you use.
- You can also view the query duration and the number of rows that are returned by the previously executed query.

  :::image type="content" source="media/ssms-connect-query-azure-sql/connection-properties.png" alt-text="Screenshot of the connection properties":::

## Additional tools

You can also use [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) to connect and query [SQL Server](../../azure-data-studio/quickstart-sql-server.md), [Azure SQL Database](../../azure-data-studio/quickstart-sql-database.md), and [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md).

## Next steps

The best way to get acquainted with SSMS is through hands-on practice. These articles help you with various features available within SSMS.

- [SQL Server Management Studio (SSMS) Query Editor](../f1-help/database-engine-query-editor-sql-server-management-studio.md)
- [Scripting](../tutorials/scripting-ssms.md)
- [Using Templates in SSMS](../template/templates-ssms.md)
- [SSMS Configuration](../tutorials/ssms-configuration.md)
- [Additional Tips and Tricks for using SSMS](../tutorials/ssms-tricks.md)
