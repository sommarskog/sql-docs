---
title: "Security (Report Builder)"
description: Report Builder security features relate to publishing locations, published reports, external data sources and models based on them, and interactive features.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: report-builder
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Security (Report Builder)

  Report Builder is a report authoring client application that is designed to work with a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] report server. The report server can be configured to work in native mode as a stand-alone server or in SharePoint integrated mode to support reports on a SharePoint site.

In Report Builder, you can author reports, shared datasets, and reusable report parts. From a report server or SharePoint site, you can edit reports and add shared data sources, shared datasets, and shared report parts.

[!INCLUDE [ssrs-report-parts-deprecated](../../includes/ssrs-report-parts-deprecated.md)]

To author, publish, and use reports and report-related items, you should understand how security features relate to the following areas:

- **The report server or SharePoint site where you publish reports** These features are managed by the report server administrator or SharePoint site administrator.

- **Published reports and report-related items** Report-related items include embedded and shared data sources and their credentials, shared datasets, parameters, report parts, and report models. Security features that apply to these items are managed by the report author. The report author must be granted sufficient permissions by the report server administrator or SharePoint site administrator to publish and share the items.

- **External data sources that are used by a report** These features are managed by the owner of the external data source.

- **Report models that are based on external data sources** These features are managed by the model designer.

- **Interactive report features such as parameters** These features are managed by the report author.

Review the information in this topic to better understand how to use security features to help manage and secure reports and report-related items.

## <a id="ReportServers"></a> Understand Security for Report Servers

Publishing reports and viewing reports are privileged operations. A report server administrator grants permissions to ensure that only authorized users can publish and view reports on one of the following types of report servers:

- Report server configured in native mode

     To connect to or browse to a report server, you must have a valid URL and have sufficient permissions to access the server.

     To view or publish items on a report server, sets of permissions that apply to report-related items and operations are organized into roles. A report server administrator assigns you to one or more roles. For example, the predefined role Browser enables you to view reports, folders, models, and resources.

     If you cannot connect to or browse to a report server, contact the report server administrator. For more information, see [Reporting Services Security and Protection](../../reporting-services/security/reporting-services-security-and-protection.md).

- Report server configured in SharePoint integrated mode

     To connect to a SharePoint site that is integrated with a report server, you must have a valid URL to the SharePoint site or subsite and have sufficient permissions to access it.

     Permission to access report-related items and operations is granted through SharePoint security policies that map a user or group account with a permission level, relative to an item.

     If you cannot connect to or browse to a SharePoint site or subsite, contact the SharePoint site administrator.

## <a id="Reports"></a> Understand Security for Published Reports and Report-related Items

Security for reports and report-related items is managed by the report server administrator. Report-related items include embedded and shared data sources including credentials, shared datasets, parameters, report parts, and models.

On a report server or SharePoint site, reports and report-related items and operations are independently securable. Permission to access items and operations is granted through security policies that map a user or group account with a permission level, relative to an item. To reduce the complexity and overhead of maintaining a large number of policies, permissions on a container, such as a folder, are inherited by items in the container. For example, if a user has the specific View Reports permission on a folder, they have View Reports permission on the items in the folder.

Permissions can be overridden on items or folders by using item level security. When item-level security is applied, permission inheritance from the parent container no longer applies to the item. If item-level security is applied to a folder, nested folders inherit the same permissions.

If you are not able to browse to and find items that someone else has published for you, you might have a permissions issue on the item or on the folder.

To enable others to browse to and find items that you published to be shared, you must work with the report server administrator to set up a folder organization that provides access to your users. Access must be available for authoring reports and for running published reports.

For more information, see the following topics:

- [Roles and Permissions (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)

- [Manage Shared Datasets](../../reporting-services/report-data/manage-shared-datasets.md)

### Update Notifications for Report Parts

Report parts are published to a report server so that others can share them. By design, you specify the location to publish report parts to.

Users who include report parts in their reports can enable the update feature. When this feature is enabled, users receive notifications when report parts change on the report server.

If report parts are moved from the original location, the update notice includes both the current location and the previous location of the report part. Accept updates only from trusted locations.

For more information, see [Report Parts (Report Builder and SSRS)](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).

## <a id="Data"></a> Understand Security for Report Data and External Data Sources

To access data from each external data source in a report, you create an embedded data source or add a reference to a shared data source or shared dataset in your report.

For each external data source, you must supply credentials that are sufficient to access the source and the underlying data. The data source owner specifies the type of credentials that provides this access.

Credentials are not saved in the report definition. They are managed independently from the report on the report server or SharePoint site and on the report authoring client.

At report design time, credentials are used to run dataset queries and preview the report. At run time, credentials are used to run the report and cache query results. You can also cache shared dataset query results independently. Design time and run time credentials might differ. For more information, see [Specify Credentials in Report Builder](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).

For more information about securing data, see [Security Center for SQL Server Database Engine and Azure SQL Database](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

For more information about data sources, see [Create data connection strings - Report Builder & SSRS](../report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).

## <a id="Models"></a> Understand Models and Security Filters

When data is retrieved from a report model that is based on external data, you can apply security filters in the model. This is a good way to secure data so that each user who runs a report can see only the data that they have permissions to.

Report parameters are not used for row-level security; they do not prevent users or groups of users from seeing specific rows of data. To apply security to the data displayed within a report, you must use security filters or model item security.

## <a id="Interactive"></a> Understand Security for Report Authoring for Interactive Features

Reports frequently use parameters to enable a user to interactively customize their view of a report. Use the following tips to help design reports that follow good practices:

- Do not use parameters that are based on query parameters and that are type **Text** unless you provide valid values. An available values list helps a user choose only valid values. Without an available values list, you cannot restrict which values a user can enter.

- Do not use the global [&UserID] to secure private data. As a report parameter, this value can be specified in a report URL by using URL access syntax. Using this value in an expression in a shared dataset prevents the dataset from being cached. For more information, see [URL Access Parameter Reference](../../reporting-services/url-access-parameter-reference.md).

After items are published to a report server, the report server administrator can help secure them by assigning role-based security or folder and item level security. For more information, see [Secure Reports and Resources](../../reporting-services/security/secure-reports-and-resources.md).

## See also

- [Install Report Builder](../install-windows/install-report-builder.md)
- [Report Parameters (Report Builder and Report Designer)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)
