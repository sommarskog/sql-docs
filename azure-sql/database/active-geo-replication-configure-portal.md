---
title: "Tutorial: Geo-replication & failover in portal"
description: Learn how to configure geo-replication for an SQL database using the Azure portal or Azure CLI, and initiate failover.
author: rajeshsetlem
ms.author: rsetlem
ms.reviewer: wiassaf, mathoma
ms.date: 06/29/2023
ms.service: sql-database
ms.subservice: high-availability
ms.topic: tutorial
ms.custom:
  - sqldbrb=1
  - devx-track-azurecli
---
# Tutorial: Configure active geo-replication and failover (Azure SQL Database)

[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

This article shows you how to configure [active geo-replication for Azure SQL Database](active-geo-replication-overview.md#active-geo-replication-terminology-and-capabilities) using the [Azure portal](https://portal.azure.com) or Azure CLI and to initiate failover.

For best practices using auto-failover groups, see [Auto-failover groups with Azure SQL Database](auto-failover-group-sql-db.md) and [Auto-failover groups with Azure SQL Managed Instance](../managed-instance/auto-failover-group-sql-mi.md).

## Prerequisites

This tutorial shows you how to configure a database for active geo-replication. To learn how to create a single database with Azure portal, Azure CLI, Azure CLI (sql up), or PowerShell, see [Quickstart: Create a single database - Azure SQL Database](single-database-create-quickstart.md?view=azuresql&preserve-view=true&tabs=azure-powershell).

## Add a secondary database

The following steps create a new secondary database in a geo-replication partnership.  

To add a secondary database, you must be the subscription owner or co-owner.

The secondary database has the same name as the primary database and has, by default, the same service tier and compute size. The secondary database can be a single database or a pooled database. For more information, see [DTU-based purchasing model](service-tiers-dtu.md) and [vCore-based purchasing model](service-tiers-vcore.md).
After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.

> [!NOTE]
> If the partner database already exists, (for example, as a result of terminating a previous geo-replication relationship) the command fails.

# [Portal](#tab/portal)

1. In the [Azure portal](https://portal.azure.com), browse to the database that you want to set up for geo-replication.

2. On the SQL Database page, select your database, scroll to **Data management**, select **Replicas**, and then select **Create replica**.

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-cli-create-geo-replica.png" alt-text="Configure geo-replication":::

3. Select or create the server for the secondary database, and configure the **Compute + storage** options if necessary. You can select any region for your secondary server, but we recommend the [paired region](/azure/availability-zones/cross-region-replication-azure).

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-portal-create-and-configure-replica.png" alt-text="{alt-text}":::

    Optionally, you can add a secondary database to an elastic pool. To create the secondary database in a pool, select **Yes** next to **Want to use SQL elastic pool?** and select a pool on the target server. A pool must already exist on the target server. This workflow doesn't create a pool.

4. Click **Review + create**, review the information, and then click **Create**.

5. The secondary database is created and the deployment process begins.

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-portal-geo-replica-deployment.png" alt-text="Screenshot that shows the deployment status of the secondary database.":::

6. When the deployment is complete, the secondary database displays its status.

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-portal-sql-database-secondary-status.png" alt-text="Screenshot that shows the secondary database status after deployment.":::

7. Return to the primary database page, and then select **Replicas**. Your secondary database is listed under **Geo replicas**.

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-sql-db-geo-replica-list.png" alt-text="Screenshot that shows the SQL database primary and geo replicas.":::

# [Azure CLI](#tab/azure-cli)

Select the database you want to set up for geo-replication. You'll need the following information:

- Your original Azure SQL database name.
- The Azure SQL server name.
- Your resource group name.
- The name of the server to create the new replica in.

> [!NOTE]
> The secondary database must have the same service tier as the primary.

You can select any region for your secondary server, but we recommend the [paired region](/azure/availability-zones/cross-region-replication-azure).

Run the [az sql db replica create](/cli/azure/sql/db/replica#az-sql-db-replica-create) command.

```azurecli
az sql db replica create --resource-group ContosoHotel --server contosoeast --name guestlist --partner-server contosowest --family Gen5 --capacity 2 --secondary-type Geo
```

Optionally, you can add a secondary database to an elastic pool. To create the secondary database in a pool, use the `--elastic-pool` parameter. A pool must already exist on the target server. This workflow doesn't create a pool.

The secondary database is created and the deployment process begins.

When the deployment is complete, you can check the status of the secondary database by running the [az sql db replica list-links](/cli/azure/sql/db/replica#az-sql-db-replica-list-links) command:

```azurecli
az sql db replica list-links --name guestlist --resource-group ContosoHotel --server contosowest
```

# [PowerShell](#tab/powershell)

Select the database you want to set up for geo-replication. You'll need the following information:

- Your original Azure SQL database name.
- The Azure SQL server name.
- Your resource group name.
- The name of the server to create the new replica in.

> [!NOTE]
> The secondary database must have the same service tier as the primary.

You can select any region for your secondary server, but we recommend the [paired region](/azure/availability-zones/cross-region-replication-azure).

As usual, begin your PowerShell session with the following cmdlets to connect your Azure account and set the subscription context:

```powershell
Connect-AzAccount
$subscriptionid = <your subscription id here>
Set-AzContext -SubscriptionId $subscriptionid

$parameters = @{
    ResourceGroupName = 'PrimaryRG'
    ServerName = 'PrimaryServer' 
    DatabaseName = 'TestDB' 
    PartnerResourceGroupName = 'SecondaryRG'
    PartnerServerName = 'SecondaryServer'
    PartnerDatabaseName = 'TestDB'
}

New-AzSqlDatabaseSecondary @parameters

```

When the deployment is complete, you can check the status of the secondary database by running the `Get-AzSqlDatabaseReplicationLink`  command:

```powershell
$parameters = @{
    ResourceGroupName = 'PrimaryRG'
    ServerName = 'PrimaryServer'
    DatabaseName = 'TestDB'
    PartnerResourceGroupName = 'SecondaryRG'
}

Get-AzSqlDatabaseReplicationLink @parameters
```
---

## Initiate a failover

The secondary database can be switched to become the primary.

# [Portal](#tab/portal)  

1. In the [Azure portal](https://portal.azure.com), browse to the primary database in the geo-replication partnership.
2. Scroll to **Data management**, and then select **Replicas**.
3. In the **Geo replicas** list, select the database you want to become the new primary, select the ellipsis, and then select **Forced failover**.

    :::image type="content" source="./media/active-geo-replication-configure-portal/azure-portal-select-forced-failover.png" alt-text="Screenshot that shows selecting forced failover from the drop-down.":::
4. Select **Yes** to begin the failover.

# [Azure CLI](#tab/azure-cli)

Run the [az sql db replica set-primary](/cli/azure/sql/db/replica#az-sql-db-replica-set-primary) command.

```azurecli
az sql db replica set-primary --name guestlist --resource-group ContosoHotel --server contosowest
```

# [PowerShell](#tab/powershell)

Run the following command:

```powershell
$parameters = @{
    ResourceGroupName = 'SecondaryRG'
    ServerName = 'SecondaryServer'
    DatabaseName = 'TestDB'
    PartnerResourceGroupName = 'PrimaryServer'
}

Set-AzSqlDatabaseSecondary @parameters -Failover
```

---
---

The command immediately switches the secondary database into the primary role. This process normally should complete within 30 seconds or less.

There's a short period during which both databases are unavailable, on the order of 0 to 25 seconds, while the roles are switched. If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary. The entire operation should take less than a minute to complete under normal circumstances.

> [!NOTE]
> This command is designed for quick recovery of the database in case of an outage. It triggers failover without data synchronization, or forced failover.  If the primary is online and committing transactions when the command is issued some data loss may occur.

## Remove secondary database

This operation permanently stops the replication to the secondary database, and changes the role of the secondary to a regular read-write database. If the connectivity to the secondary database is broken, the command succeeds but the secondary doesn't become read-write until after connectivity is restored.

# [Portal](#tab/portal)  

1. In the [Azure portal](https://portal.azure.com), browse to the primary database in the geo-replication partnership.
2. Select **Replicas**.
3. In the **Geo replicas** list, select the database you want to remove from the geo-replication partnership, select the ellipsis, and then select **Stop replication**.
5. A confirmation window opens. Click **Yes** to remove the database from the geo-replication partnership. (Set it to a read-write database not part of any replication.)
 
# [Azure CLI](#tab/azure-cli)

Run the [az sql db replica delete-link](/cli/azure/sql/db/replica#az-sql-db-replica-delete-link) command.

```azurecli
az sql db replica delete-link --name guestlist --resource-group ContosoHotel --server contosoeast --partner-server contosowest
```

Confirm that you want to perform the operation.

# [PowerShell](#tab/powershell)

Run the following command:

```powershell
$parameters = @{
    ResourceGroupName = 'SecondaryRG'
    ServerName = 'SecondaryServer'
    DatabaseName = 'TestDB'
    PartnerResourceGroupName = 'PrimaryRG'
    PartnerServerName = 'PrimaryServer'
}
Remove-AzSqlDatabaseSecondary @parameters
```

---

## Next steps

* To learn more about active geo-replication, see [active geo-replication](active-geo-replication-overview.md).
* To learn about auto-failover groups, see [Auto-failover groups](auto-failover-group-sql-db.md)
* For a business continuity overview and scenarios, see [Business continuity overview](business-continuity-high-availability-disaster-recover-hadr-overview.md).
