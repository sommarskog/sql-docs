---
title: Microsoft Defender for SQL
description: Learn about functionality for managing your database vulnerabilities and detecting anomalous activities that could indicate a threat to your database in Azure SQL Database, Azure SQL Managed Instance, or Azure Synapse.
author: cesanu
ms.author: cesanu
ms.reviewer: maghan
ms.date: 07/04/2023
ms.service: sql-db-mi
ms.subservice: security
ms.topic: conceptual
ms.custom: sqldbrb=2
monikerRange: "= azuresql || = azuresql-db || = azuresql-mi"
---

# Microsoft Defender for SQL

[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]

Microsoft Defender for SQL is a Defender plan in Microsoft Defender for Cloud. Microsoft Defender for SQL includes functionality for surfacing and mitigating potential database vulnerabilities, and detecting anomalous activities that could indicate a threat to your database. It provides a single go-to location for enabling and managing these capabilities.

## What are the benefits of Microsoft Defender for SQL?

Microsoft Defender for SQL provides a set of advanced SQL security capabilities, including SQL Vulnerability Assessment and Advanced Threat Protection.

- [Vulnerability Assessment](/azure/defender-for-cloud/sql-azure-vulnerability-assessment-overview) is an easy-to-configure service that can discover, track, and help you remediate potential database vulnerabilities. It provides visibility into your security state, and it includes actionable steps to resolve security issues and enhance your database fortifications.
- [Advanced Threat Protection](threat-detection-overview.md) detects anomalous activities indicating unusual and potentially harmful attempts to access or exploit your database. It continuously monitors your database for suspicious activities, and it provides immediate security alerts on potential vulnerabilities, Azure SQL injection attacks, and anomalous database access patterns. Advanced Threat Protection alerts provide details of the suspicious activity and recommend action on how to investigate and mitigate the threat.

Enable Microsoft Defender for SQL once to enable all these included features. With one select, you can enable Microsoft Defender for all databases on your [server](logical-servers.md) in Azure or in your SQL Managed Instance. Enabling or managing Microsoft Defender for SQL settings requires belonging to the [SQL security manager](/azure/role-based-access-control/built-in-roles#sql-security-manager) role, or one of the database or server admin roles.

For more information about Microsoft Defender for SQL pricing, see the [Microsoft Defender for Cloud pricing page](https://azure.microsoft.com/pricing/details/security-center/).

## Enable Microsoft Defender for SQL

There are multiple ways to enable Microsoft Defender plans. You can enable it at the subscription level (**recommended**) either:

- [In Microsoft Defender for Cloud in the Azure portal](#enable-microsoft-defender-for-azure-sql-database-at-the-subscription-level-in-microsoft-defender-for-cloud)
- [Programmatically with the REST API, Azure CLI, PowerShell, or Azure Policy](#enable-microsoft-defender-plans-programatically)

Alternatively, you can enable it at the resource level as described in [Enable Microsoft Defender for Azure SQL Database at the resource level](#enable-microsoft-defender-for-azure-sql-database-at-the-resource-level).

When you enable on the subscription level, all databases in Azure SQL Database and Azure SQL Managed Instance are protected. You can then disable them individually if you choose. If you want to manually manage which databases are protected, disable at the subscription level and enable each database that you want protected.

### Enable Microsoft Defender for Azure SQL Database at the subscription level in Microsoft Defender for Cloud

To enable Microsoft Defender for Azure SQL Database at the subscription level from within Microsoft Defender for Cloud:

1. From the [Azure portal](https://portal.azure.com), open **Defender for Cloud**.
1. From Defender for Cloud's menu, select **Environment Settings**.
1. Select the relevant subscription.
1. Change the plan setting to **On**.

    :::image type="content" source="media/azure-defender-for-sql/defender-sql-subscription-level.png" alt-text="Screenshot showing enabling Microsoft Defender for Azure SQL Database at the subscription level." lightbox="media/azure-defender-for-sql/defender-sql-subscription-level.png":::

1. Select **Save**.

### Enable Microsoft Defender plans programatically

The flexibility of Azure allows for several programmatic methods for enabling Microsoft Defender plans.

Use any of the following tools to enable Microsoft Defender for your subscription:

| Method | Instructions |
| --- | --- |
| REST API | [Pricings API](/rest/api/securitycenter/pricings) |
| Azure CLI | [az security pricing](/cli/azure/security/pricing) |
| PowerShell | [Set-AzSecurityPricing](/powershell/module/az.security/set-azsecuritypricing) |
| Azure Policy | [Bundle Pricings](https://github.com/Azure/Azure-Security-Center/blob/master/Pricing%20%26%20Settings/ARM%20Templates/Set-ASC-Bundle-Pricing.json) |

### Enable Microsoft Defender for Azure SQL Database at the resource level

We recommend enabling Microsoft Defender plans at the subscription level so that new resources are automatically protected. However, if you have an organizational reason to enable Microsoft Defender for Cloud at the server level, use the following steps:

1. From the [Azure portal](https://portal.azure.com), open your server or managed instance.
1. Under the **Security** heading, select **Defender for Cloud**.
1. Select **Enable Microsoft Defender for SQL**.

    :::image type="content" source="media/azure-defender-for-sql/enable-defender-sql.png" alt-text="Screenshot showing Enable Microsoft Defender for SQL from within Azure SQL databases." lightbox="media/azure-defender-for-sql/enable-defender-sql.png":::

> [!NOTE]  
> A storage account is automatically created and configured to store your **Vulnerability Assessment** scan results. If you've already enabled Microsoft Defender for another server in the same resource group and region, then the existing storage account is used.
>  
> The cost of Microsoft Defender for SQL is aligned with Microsoft Defender for Cloud standard tier pricing per node, where a node is the entire server or managed instance. You are thus paying only once for protecting all databases on the server or managed instance with Microsoft Defender for SQL. You can evaluate Microsoft Defender for Cloud with a free trial.

## Manage Microsoft Defender for SQL settings

To view and manage Microsoft Defender for SQL settings:

1. From the **Security** area of your server or managed instance, select **Defender for Cloud**.

    On this page, you see the status of Microsoft Defender for SQL (disabled or enabled):

    :::image type="content" source="media/azure-defender-for-sql/enable-defender-sql-enabled-disabled.png" alt-text="Screenshot showing status as enabled or disabled." lightbox="media/azure-defender-for-sql/enable-defender-sql-enabled-disabled.png":::

1. If Microsoft Defender for SQL is enabled, you see a **Configure** link as shown in the previous graphic. To edit the settings for Microsoft Defender for SQL, select **Configure**.

    :::image type="content" source="media/azure-defender-for-sql/defender-sql-configure.png" alt-text="Screenshot showing Configure screen for Microsoft Defender for SQL." lightbox="media/azure-defender-for-sql/defender-sql-configure.png":::

1. Make the necessary changes and select **Save**.

## Next steps

- Learn more about [Vulnerability Assessment](/azure/defender-for-cloud/sql-azure-vulnerability-assessment-overview)
- Learn more about [Advanced Threat Protection](threat-detection-configure.md)
- Learn more about [Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction)
