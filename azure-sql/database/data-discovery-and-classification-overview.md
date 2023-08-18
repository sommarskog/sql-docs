---
title: Data Discovery & Classification
titleSuffix: Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse
description: Data Discovery & Classification for Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse Analytics
author: Madhumitatripathy
ms.author: matripathy
ms.reviewer: wiassaf, vanto, mathoma
ms.date: 09/14/2022
ms.service: sql-db-mi
ms.subservice: security
ms.topic: conceptual
ms.custom: sqldbrb=1
tags: azure-synapse
---
# Data Discovery & Classification
[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]

Data Discovery & Classification is built into Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse Analytics. It provides basic capabilities for discovering, classifying, labeling, and reporting the sensitive data in your databases.

Your most sensitive data might include business, financial, healthcare, or personal information. It can serve as infrastructure for:

- Helping to meet standards for data privacy and requirements for regulatory compliance.
- Various security scenarios, such as monitoring (auditing) access to sensitive data.
- Controlling access to and hardening the security of databases that contain highly sensitive data.

> [!NOTE]
> For information about SQL Server on-premises, see [SQL Data Discovery & Classification](/sql/relational-databases/security/sql-data-discovery-and-classification).

## <a id="what-is-dc"></a>What is Data Discovery & Classification?

Data Discovery & Classification currently supports the following capabilities:

- **Discovery and recommendations:** The classification engine scans your database and identifies columns that contain potentially sensitive data. It then provides you with an easy way to review and apply recommended classification via the Azure portal.

- **Labeling:** You can apply sensitivity-classification labels persistently to columns by using new metadata attributes that have been added to the SQL Server database engine. This metadata can then be used for sensitivity-based auditing scenarios.

- **Query result-set sensitivity:** The sensitivity of a query result set is calculated in real time for auditing purposes.

- **Visibility:** You can view the database-classification state in a detailed dashboard in the Azure portal. Also, you can download a report in Excel format to use for compliance and auditing purposes and other needs.

## <a id="discover-classify-columns"></a>Discover, classify, and label sensitive columns

This section describes the steps for:

- Discovering, classifying, and labeling columns that contain sensitive data in your database.
- Viewing the current classification state of your database and exporting reports.

The classification includes two metadata attributes:

- **Labels**: The main classification attributes, used to define the sensitivity level of the data stored in the column.  
- **Information types**: Attributes that provide more granular information about the type of data stored in the column.

### Information Protection policy

Azure SQL offers both SQL Information Protection policy and Microsoft Information Protection policy in data classification, and you can choose either of these two policies based on your requirement.

:::image type="content" source="./media/data-discovery-and-classification-overview/protection-policy-types.png" alt-text="Screenshot of Information Protection policy types." lightbox="./media/data-discovery-and-classification-overview/protection-policy-types.png":::

### SQL Information Protection policy

Data Discovery & Classification comes with a built-in set of sensitivity labels and information types with discovery logic which is native to the SQL logical server. You can continue using the protection labels available in the default policy file, or you can customize this taxonomy. You can define a set and ranking of classification constructs specifically for your environment.

### Define and customize your classification taxonomy

You define and customize of your classification taxonomy in one central place for your entire Azure organization. That location is in [Microsoft Defender for Cloud](/azure/security-center/security-center-introduction), as part of your security policy. Only someone with administrative rights on the organization's root management group can do this task.

As part of policy management, you can define custom labels, rank them, and associate them with a selected set of information types. You can also add your own custom information types and configure them with string patterns. The patterns are added to the discovery logic for identifying this type of data in your databases.

For more information, see [Customize the SQL information protection policy in Microsoft Defender for Cloud (Preview)](/azure/security-center/security-center-info-protection-policy).

After the organization-wide policy has been defined, you can continue classifying individual databases by using your customized policy.

### Classify database in SQL Information Protection policy mode

> [!NOTE]
> The below example uses Azure SQL Database, but you should select the appropriate product that you want to configure Data Discovery & Classification.

1. Go to the [Azure portal](https://portal.azure.com).

1. Go to **Data Discovery & Classification** under the **Security** heading in your Azure SQL Database pane. The Overview tab includes a summary of the current classification state of the database. The summary includes a detailed list of all classified columns, which you can also filter to show only specific schema parts, information types, and labels. If you haven't classified any columns yet, [skip to step 4](#step-4).

    ![Overview](./media/data-discovery-and-classification-overview/data-discovery-and-classification.png)

1. To download a report in Excel format, select **Export** in the top menu of the pane.

1. <a id="step-4"></a>To begin classifying your data, select the **Classification** tab on the **Data Discovery & Classification** page.

    The classification engine scans your database for columns containing potentially sensitive data and provides a list of recommended column classifications.

1. View and apply classification recommendations:

   - To view the list of recommended column classifications, select the recommendations panel at the bottom of the pane.

   - To accept a recommendation for a specific column, select the check box in the left column of the relevant row. To mark all recommendations as accepted, select the leftmost check box in the recommendations table header.

   - To apply the selected recommendations, select **Accept selected recommendations**.

   ![Recommendations for classification](./media/data-discovery-and-classification-overview/recommendation.png)

1. You can also classify columns manually, as an alternative or in addition to the recommendation-based classification:

   1. Select **Add classification** in the top menu of the pane.

   1. In the context window that opens, select the schema, table, and column that you want to classify, and the information type and sensitivity label.

   1. Select **Add classification** at the bottom of the context window.

   ![Manually add classification](./media/data-discovery-and-classification-overview/manually-add-classification.png)


1. To complete your classification and persistently label (tag) the database columns with the new classification metadata, select **Save** in the **Classification** page.

### Microsoft Information Protection policy

Microsoft Information Protection (MIP) labels provide a simple and uniform way for users to classify sensitive data uniformly across different Microsoft applications. MIP sensitivity labels are created and managed in [Microsoft 365 compliance center](https://compliance.microsoft.com/). To learn how to create and publish MIP sensitive labels in Microsoft 365 compliance center, see the article, [Create and publish sensitivity labels](/microsoft-365/compliance/create-sensitivity-labels).

#### Prerequisites to switch to MIP policy

- The current user has tenant wide **Security Admin** permissions to apply policy at the tenant root management group level. For more information, see [Grant tenant-wide permissions to yourself](/azure/defender-for-cloud/tenant-wide-permissions-management#grant-tenant-wide-permissions-to-yourself).
  :::image type="content" source="media/data-discovery-and-classification-overview/request-security-admin-permissions.png" alt-text="Screenshot of Azure portal request for tenant level Security Admin permissions.":::
- Your tenant has an active Microsoft 365 subscription and you have labels published for the current user. For more information, see [Create and configure sensitivity labels and their policies](/microsoft-365/compliance/create-sensitivity-labels).

### Classify database in Microsoft Information Protection policy mode

1. Go to the [Azure portal](https://portal.azure.com).
1. Navigate to your database in Azure SQL Database
1. Go to **Data Discovery & Classification** under the **Security** heading in your database pane.
1. To select **Microsoft Information Protection policy**, select the **Overview** tab, and select **Configure**.
1. Select **Microsoft Information Protection policy** in the **Information Protection policy** options, and select **Save**.

   :::image type="content" source="./media/data-discovery-and-classification-overview/select-microsoft-information-protection-policy.png" alt-text="Screenshot of selecting Microsoft Information Protection policy for Azure SQL Database." lightbox="./media/data-discovery-and-classification-overview/select-microsoft-information-protection-policy.png":::

1. If you go to the **Classification** tab, or select **Add classification**, you will now see M365 sensitivity labels appear in the **Sensitivity label** dropdown.

   :::image type="content" source="./media/data-discovery-and-classification-overview/select-sensitivity-label.png" alt-text="Screenshot of Sensitivity label dropdown.":::

   :::image type="content" source="./media/data-discovery-and-classification-overview/sensitivity-label-classification-tab.png" alt-text="Screenshot of Sensitivity label in the Classification tab." lightbox="./media/data-discovery-and-classification-overview/sensitivity-label-classification-tab.png":::

- Information type is `[n/a]` while you are in MIP policy mode and automatic data discovery & recommendations remain disabled.
- A warning icon may appear against an already classified column if the column was classified using a different Information Protection policy than the currently active policy. For example, if the column was classified with a label using SQL Information Protection policy earlier and now you are in Microsoft Information Protection policy mode. You will see a warning icon against that specific column. This warning icon does not indicate any problem, but is used only for information purposes.

   :::image type="content" source="./media/data-discovery-and-classification-overview/classification-warning.png" alt-text="Screenshot of warnings for classified columns because of different Information Protection policies." lightbox="./media/data-discovery-and-classification-overview/classification-warning.png":::

## <a id="audit-sensitive-data"></a>Audit access to sensitive data

An important aspect of the classification is the ability to monitor access to sensitive data. [Azure SQL Auditing](../../azure-sql/database/auditing-overview.md) has been enhanced to include a new field in the audit log called `data_sensitivity_information`. This field logs the sensitivity classifications (labels) of the data that was returned by a query. Here's an example:

[![Audit log](./media/data-discovery-and-classification-overview/11_data_classification_audit_log.png)](./media/data-discovery-and-classification-overview/11_data_classification_audit_log.png#lightbox)

These are the activities that are actually auditable with sensitivity information:
- ALTER TABLE ... DROP COLUMN
- BULK INSERT
- SELECT
- DELETE
- INSERT
- MERGE
- UPDATE
- UPDATETEXT
- WRITETEXT
- DROP TABLE
- BACKUP
- DBCC CloneDatabase
- SELECT INTO
- INSERT INTO EXEC
- TRUNCATE TABLE
- DBCC SHOW_STATISTICS
- sys.dm_db_stats_histogram

Use [sys.fn_get_audit_file](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql) to return information from an audit file stored in an Azure Storage account.

## <a id="permissions"></a>Permissions

These built-in roles can read the data classification of a database:

- Owner
- Reader
- Contributor
- SQL Security Manager
- User Access Administrator

These are the required actions to read the data classification of a database are:

- Microsoft.Sql/servers/databases/currentSensitivityLabels/*
- Microsoft.Sql/servers/databases/recommendedSensitivityLabels/*
- Microsoft.Sql/servers/databases/schemas/tables/columns/sensitivityLabels/*

These built-in roles can modify the data classification of a database:

- Owner
- Contributor
- SQL Security Manager

This is the required action to modify the data classification of a database are:

- Microsoft.Sql/servers/databases/schemas/tables/columns/sensitivityLabels/*

Learn more about role-based permissions in [Azure RBAC](/azure/role-based-access-control/overview).

> [!NOTE]
> The Azure SQL built-in roles in this section apply to a dedicated SQL pool (formerly SQL DW) but are not available for dedicated SQL pools and other SQL resources within Azure Synapse workspaces. For SQL resources in Azure Synapse workspaces, use the available actions for data classification to create custom Azure roles as needed for labelling. For more information on the `Microsoft.Synapse/workspaces/sqlPools` provider operations, see [Microsoft.Synapse](/azure/role-based-access-control/resource-provider-operations#microsoftsynapse).

## Manage classifications

You can use T-SQL, a REST API, or PowerShell to manage classifications.

### Use T-SQL

You can use T-SQL to add or remove column classifications, and to retrieve all classifications for the entire database.

> [!NOTE]
> When you use T-SQL to manage labels, there's no validation that labels that you add to a column exist in the organization's information-protection policy (the set of labels that appear in the portal recommendations). So, it's up to you to validate this.

For information about using T-SQL for classifications, see the following references:

- To add or update the classification of one or more columns: [ADD SENSITIVITY CLASSIFICATION](/sql/t-sql/statements/add-sensitivity-classification-transact-sql)
- To remove the classification from one or more columns: [DROP SENSITIVITY CLASSIFICATION](/sql/t-sql/statements/drop-sensitivity-classification-transact-sql)
- To view all classifications on the database: [sys.sensitivity_classifications](/sql/relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql)

### Use PowerShell cmdlets
Manage classifications and recommendations for Azure SQL Database and Azure SQL Managed Instance using PowerShell.

#### PowerShell cmdlets for Azure SQL Database

- [Get-AzSqlDatabaseSensitivityClassification](/powershell/module/az.sql/get-azsqldatabasesensitivityclassification)
- [Set-AzSqlDatabaseSensitivityClassification](/powershell/module/az.sql/set-azsqldatabasesensitivityclassification)
- [Remove-AzSqlDatabaseSensitivityClassification](/powershell/module/az.sql/remove-azsqldatabasesensitivityclassification)
- [Get-AzSqlDatabaseSensitivityRecommendation](/powershell/module/az.sql/get-azsqldatabasesensitivityrecommendation)
- [Enable-AzSqlDatabaSesensitivityRecommendation](/powershell/module/az.sql/enable-azsqldatabasesensitivityrecommendation)
- [Disable-AzSqlDatabaseSensitivityRecommendation](/powershell/module/az.sql/disable-azsqldatabasesensitivityrecommendation)

#### PowerShell cmdlets for Azure SQL Managed Instance

- [Get-AzSqlInstanceDatabaseSensitivityClassification](/powershell/module/az.sql/get-azsqlinstancedatabasesensitivityclassification)
- [Set-AzSqlInstanceDatabaseSensitivityClassification](/powershell/module/az.sql/set-azsqlinstancedatabasesensitivityclassification)
- [Remove-AzSqlInstanceDatabaseSensitivityClassification](/powershell/module/az.sql/remove-azsqlinstancedatabasesensitivityclassification)
- [Get-AzSqlInstanceDatabaseSensitivityRecommendation](/powershell/module/az.sql/get-azsqlinstancedatabasesensitivityrecommendation)
- [Enable-AzSqlInstanceDatabaseSensitivityRecommendation](/powershell/module/az.sql/enable-azsqlinstancedatabasesensitivityrecommendation)
- [Disable-AzSqlInstanceDatabaseSensitivityRecommendation](/powershell/module/az.sql/disable-azsqlinstancedatabasesensitivityrecommendation)

### Use the REST API

You can use the REST API to programmatically manage classifications and recommendations. The published REST API supports the following operations:

- [Create Or Update](/rest/api/sql/sensitivitylabels/createorupdate): Creates or updates the sensitivity label of the specified column.
- [Delete](/rest/api/sql/sensitivitylabels/delete): Deletes the sensitivity label of the specified column.
- [Disable Recommendation](/rest/api/sql/sensitivitylabels/disablerecommendation): Disables sensitivity recommendations on the specified column.
- [Enable Recommendation](/rest/api/sql/sensitivitylabels/enablerecommendation): Enables sensitivity recommendations on the specified column. (Recommendations are enabled by default on all columns.)
- [Get](/rest/api/sql/sensitivitylabels/get): Gets the sensitivity label of the specified column.
- [List Current By Database](/rest/api/sql/sensitivitylabels/listcurrentbydatabase): Gets the current sensitivity labels of the specified database.
- [List Recommended By Database](/rest/api/sql/sensitivitylabels/listrecommendedbydatabase): Gets the recommended sensitivity labels of the specified database.

## Retrieve classifications metadata using SQL drivers

You can use the following SQL drivers to retrieve classification metadata:

- [Microsoft.Data.SqlClient](/sql/connect/ado-net/sql/data-classification)
- [ODBC Driver](/sql/connect/odbc/data-classification)
- [OLE DB Driver](/sql/connect/oledb/features/using-data-classification)
- [JDBC Driver](/sql/connect/jdbc/data-discovery-classification-sample)
- [Microsoft Drivers for PHP for SQL Server](/sql/connect/php/release-notes-php-sql-driver)

## FAQ - Advanced classification capabilities

**Question**: Will [Microsoft Purview](/azure/purview/overview) replace SQL Data Discovery & Classification or will SQL Data Discovery & Classification be retired soon?
**Answer**: We continue to support SQL Data Discovery & Classification and encourage you to adopt [Microsoft Purview](/azure/purview/overview) which has richer capabilities to drive advanced classification capabilities and data governance. If we decide to retire any service, feature, API or SKU, you will receive advance notice including a migration or transition path. Learn more about Microsoft Lifecycle policies [here](/lifecycle/index).

## Next steps

- Consider configuring [Azure SQL Auditing](../../azure-sql/database/auditing-overview.md) for monitoring and auditing access to your classified sensitive data.
- For a presentation that includes data Discovery & Classification, see [Discovering, classifying, labeling & protecting SQL data | Data Exposed](https://www.youtube.com/watch?v=itVi9bkJUNc).
- To classify your Azure SQL Databases and Azure Synapse Analytics with Microsoft Purview labels using T-SQL commands, see [Classify your Azure SQL data using Microsoft Purview labels](/azure/sql-database/scripts/sql-database-import-purview-labels).
