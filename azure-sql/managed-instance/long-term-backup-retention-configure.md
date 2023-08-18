---
title: Azure SQL Managed Instance long-term backup retention
description: Learn how to store and restore automated backups on separate Azure Blob storage containers for an Azure SQL Managed Instance using the Azure portal and PowerShell.
author: Stralle
ms.author: strrodic
ms.reviewer: mathoma
ms.date: 03/25/2023
ms.service: sql-managed-instance
ms.subservice: backup-restore
ms.topic: how-to
ms.custom:
  - devx-track-azurepowershell
  - devx-track-azurecli
---
# Manage Azure SQL Managed Instance long-term backup retention
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

In Azure SQL Managed Instance, you can configure a [long-term backup retention](../database/long-term-retention-overview.md) policy (LTR). This allows you to automatically retain database backups in separate Azure Blob storage containers for up to 10 years. You can then recover a database using these backups with the Azure portal and PowerShell.

The following sections show you how to use the Azure portal, PowerShell, and Azure CLI to configure the long-term backup retention, view backups in Azure SQL storage, and restore from a backup in Azure SQL storage.

## Prerequisites

# [Portal](#tab/portal)

An active Azure subscription.

# [Azure CLI](#tab/azure-cli)

Prepare your environment for the Azure CLI.

[!INCLUDE[azure-cli-prepare-your-environment-no-header](~/../azure-sql/reusable-content/azure-cli/azure-cli-prepare-your-environment-no-header.md)]

# [PowerShell](#tab/powershell)

Prepare your environment for PowerShell.

[!INCLUDE [updated-for-az](../includes/updated-for-az.md)]

> [!IMPORTANT]
> The PowerShell Azure Resource Manager module is still supported by Azure SQL Database, however, future development will be done in the Az.Sql module. For these cmdlets, see [AzureRM.Sql](/powershell/module/AzureRM.Sql/). The arguments for the commands in the Az module and in the AzureRm modules are substantially identical.

For **Get-AzSqlInstanceDatabaseLongTermRetentionBackup** and **Restore-AzSqlInstanceDatabase**, you will need to have one of the following roles:

- Subscription Owner role or
- SQL Managed Instance Contributor role or
- Custom role with the following permissions:
  - `Microsoft.Sql/locations/longTermRetentionManagedInstanceBackups/read`
  - `Microsoft.Sql/locations/longTermRetentionManagedInstances/longTermRetentionManagedInstanceBackups/read`
  - `Microsoft.Sql/locations/longTermRetentionManagedInstances/longTermRetentionDatabases/longTermRetentionManagedInstanceBackups/read`

For **Remove-AzSqlInstanceDatabaseLongTermRetentionBackup**, you will need to have one of the following roles:

- Subscription Owner role or
- Custom role with the following permission:
  - `Microsoft.Sql/locations/longTermRetentionManagedInstances/longTermRetentionDatabases/longTermRetentionManagedInstanceBackups/delete`

> [!NOTE]
> The SQL Managed Instance Contributor role does not have permission to delete LTR backups.

Azure RBAC permissions could be granted in either *subscription* or *resource group* scope. However, to access LTR backups that belong to a dropped instance, the permission must be granted in the *subscription* scope of that instance.

- `Microsoft.Sql/locations/longTermRetentionManagedInstances/longTermRetentionDatabases/longTermRetentionManagedInstanceBackups/delete`

---

## Create long-term retention policies

You can configure SQL Managed Instance to [retain automated backups](../database/long-term-retention-overview.md) for a period longer than the retention period for your service tier.

# [Portal](#tab/portal)

1. In the Azure portal, select your managed instance and then click **Backups**. On the **Retention policies** tab, select the database(s) on which you want to set or modify long-term backup retention policies. Changes will not apply to any databases left unselected. 

   ![manage backups link](./media/long-term-backup-retention-configure/ltr-configure-ltr.png)

2. In the **Configure policies** pane, specify your desired retention period for weekly, monthly, or yearly backups. Choose a retention period of '0' to indicate that no long-term backup retention should be set.

   ![configure policies](./media/long-term-backup-retention-configure/ltr-configure-policies.png)

3. When complete, click **Apply**.

> [!IMPORTANT]
> When you enable a long-term backup retention policy, it may take up to 7 days for the first backup to become visible and available to restore. For details of the LTR backup cadence, see [long-term backup retention](../database/long-term-retention-overview.md).

# [Azure CLI](#tab/azure-cli)

1. Run the [az sql midb show](/cli/azure/sql/midb#az-sql-midb-show) command to get the details for the SQL Managed Instance database.

    ```azurecli
    az sql midb show /
    --resource-group mygroup /
    --managed-instance myinstance /
    --name mymanageddb /
    --subscription mysubscription
    ```

2. Run the [az sql midb ltr-policy set](/cli/azure/sql/midb/ltr-policy#az-sql-midb-ltr-policy-set) command to create an LTR policy. The following example sets a long-term retention policy for 12 weeks for the weekly backup.

    ```azurecli
    az sql midb ltr-policy set /
    --resource-group mygroup /
    --managed-instance myinstance /
    --name mymanageddb /
    --weekly-retention "P12W"
    ```

    This example sets a retention policy for 12 weeks for the weekly backup, 5 years for the yearly backup, and the week of April 15 in which to take the yearly LTR backup.

    ```azurecli
    az sql midb ltr-policy set /
    --resource-group mygroup /
    --managed-instance myinstance /
    --name mymanageddb /
    --weekly-retention "P12W" /
    --yearly-retention "P5Y" /
    --week-of-year 16
    ```

# [PowerShell](#tab/powershell)

```powershell
# get the Managed Instance
$subId = "<subscriptionId>"
$instanceName = "<instanceName>"
$resourceGroup = "<resourceGroupName>"
$dbName = "<databaseName>"

Connect-AzAccount

Select-AzSubscription -SubscriptionId $subId

$instance = Get-AzSqlInstance -Name $instanceName -ResourceGroupName $resourceGroup

# create LTR policy with WeeklyRetention = 12 weeks. MonthlyRetention and YearlyRetention = 0 by default.
$LTRPolicy = @{
    InstanceName = $instanceName 
    DatabaseName = $dbName 
    ResourceGroupName = $resourceGroup 
    WeeklyRetention = 'P12W'
}
Set-AzSqlInstanceDatabaseBackupLongTermRetentionPolicy @LTRPolicy

# create LTR policy with WeeklyRetention = 12 weeks, YearlyRetention = 5 years and WeekOfYear = 16 (week of April 15). MonthlyRetention = 0 by default.
$LTRPolicy = @{
    InstanceName = $instanceName 
    DatabaseName = $dbName 
    ResourceGroupName = $resourceGroup 
    WeeklyRetention = 'P12W' 
    YearlyRetention = 'P5Y' 
    WeekOfYear = '16'
}
Set-AzSqlInstanceDatabaseBackupLongTermRetentionPolicy @LTRPolicy
```

---

## View backups and restore from a backup

# [Portal](#tab/portal)


To view available long-term backups from the Azure portal, follow these steps: 

1. In the Azure portal, select your managed instance and then select **Backups**. On the **Available backups** tab, select the database for which you want to see available backups. Select **Manage**.

   ![select database](./media/long-term-backup-retention-configure/ltr-available-backups-select-database.png)

1. In the **Manage backups** pane, review the available backups.

   ![view backups](./media/long-term-backup-retention-configure/ltr-available-backups.png)

You can also restore from this page by choosing the backup and selecting **Restore**. 

Alternatively, to restore a backup from long-term retention by using the Azure portal, follow these steps: 

1. Sign in to the [Azure portal](https://portal.azure.com).
1. Go to the target SQL Managed Instance where you plan to restore your database to. 
1. On the **Overview** page, choose **+ New database** to open the **Create Azure SQL Managed Database** page. 

   :::image type="content" source="media/point-in-time-restore/choose-database-to-restore.png" alt-text="Screenshot that shows the SQL Managed Instance overview pane in the Azure portal, with adding a new database selected. ":::

1. On the **Basics** tab of the **Create Azure SQL Managed Database page**, provide subscription and resource group details under **Project details**. Then, under **Database details** provide the new name of the database you plan to restore. Confirm the correct managed instance is listed in the drop down. Then select **Next: Data source >**

    :::image type="content" source="./media/point-in-time-restore/create-database-page.png" alt-text="Screenshot of the Azure portal that shows the Basics tab of the Create Azure SQL Managed Database page.":::

1. On the **Data source** tab, choose **Point-in-time restore** under **Use existing data**. Provide the subscription, resource group and managed instance that contains the source database. From the **Managed database** drop-down, choose the database you want to restore, and then choose the point in time you want to restore the database from. The source and target instance can be the same, or two different instances. Select **Next : Additional settings >**

    :::image type="content" source="./media/long-term-backup-retention-configure/restore-long-term-backup.png" alt-text="Screenshot of the Azure portal that shows the data source tab of the Create Azure SQL Managed Database page, with long-term retention selected.":::

1. On the **Additional settings** tab, you can check the box to inherit the retention policy from the source database, or, alternatively, you can select **Configure retention** to open the **Configure policies** page, and set your desired retention policies for your restored database. When finished, select **Review + create**. 

    :::image type="content" source="./media/point-in-time-restore/additional-settings-page.png" alt-text="Screenshot of the Azure portal that shows the additional settings tab of the Create Azure SQL Managed Database page.":::

1. On **Review + create**, when validation is successful, select **Create** to restore your database.

This action starts the restore process, which creates a new database and populates it with data from the original database at the specified point in time. For more information about the recovery process, see [Recovery time](../database/recovery-using-backups.md#recovery-time).

> [!NOTE]
> From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](../database/recovery-using-backups.md#point-in-time-restore).

# [Azure CLI](#tab/azure-cli)

### View LTR policies

Run the [az sql midb ltr-policy show](/cli/azure/sql/midb/ltr-policy#az-sql-midb-ltr-policy-show) command to view the LTR policy for a single database within an instance.

```azurecli
az sql midb ltr-policy show \
    --resource-group mygroup \
    --managed-instance myinstance \
    --name mymanageddb
```

### View LTR backups

Use the [az sql midb ltr-backup list](/cli/azure/sql/midb/ltr-backup#az-sql-midb-ltr-backup-list) command to view the LTR backups within an instance.

```azurecli
az sql midb ltr-backup list \
    --resource-group mygroup \
    --location eastus2 \
    --managed-instance myinstance
```

### Delete LTR backups

Run the [az sql midb ltr-backup delete](/cli/azure/sql/midb/ltr-backup#az-sql-midb-ltr-backup-delete) command to remove an LTR backup. You can run [az sql midb ltr-backup list](/cli/azure/sql/midb/ltr-backup#az-sql-midb-ltr-backup-list) to get the backup `name`.

```azurecli
az sql midb ltr-backup delete \
    --location eastus2 \
    --managed-instance myinstance \
    --database mymanageddb \
    --name "3214b3fb-fba9-43e7-96a3-09e35ffcb336;132292152080000000"
```

> [!IMPORTANT]
> Deleting LTR backup is non-reversible. To delete an LTR backup after the instance has been deleted you must have Subscription scope permission. You can set up notifications about each delete in Azure Monitor by filtering for operation 'Deletes a long term retention backup'. The activity log contains information on who and when made the request. See [Create activity log alerts](/azure/azure-monitor/alerts/alerts-activity-log) for detailed instructions.

### Restore from LTR backups

Run the [az sql midb ltr-backup restore](/cli/azure/sql/midb/ltr-backup#az-sql-midb-ltr-backup-restore) command to restore your database from an LTR backup. You can run [az sql midb ltr-backup show](/cli/azure/sql/midb/ltr-backup#az-sql-midb-ltr-backup-show) to get the `backup-id`.

1. Create a variable for the `backup-id` with the command `az sql db ltr-backup show` for future use.

   ```azurecli
    get_backup_id=$(az sql midb ltr-backup show
       --location eastus2 \
       --managed-instance myinstance \
       --database mydb \
       --name "3214b3fb-fba9-43e7-96a3-09e35ffcb336;132292152080000000" \
       --query 'id' \
       --output tsv)
   ```
2. Restore your database from an LTR backup

    ```azurecli
    az sql midb ltr-backup restore \
        --dest-database targetmidb \
        --dest-mi myinstance \
        --dest-resource-group mygroup \
        --backup-id $get_backup_id
    ```

> [!IMPORTANT]
> To restore from an LTR backup after the instance has been deleted, you must have permissions scoped to the subscription of the instance and that subscription must be active.

> [!NOTE]
> From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name. See [point in time restore](../database/recovery-using-backups.md#point-in-time-restore).

# [PowerShell](#tab/powershell)

### View LTR policies

This example shows how to list the LTR policies within an instance for a single database.

```powershell
# gets the current version of LTR policy for a database
$LTRPolicy = @{
    InstanceName = $instanceName 
    DatabaseName = $dbName 
    ResourceGroupName = $resourceGroup
}
Get-AzSqlInstanceDatabaseBackupLongTermRetentionPolicy @LTRPolicy 
```

This example shows how to list the LTR policies for all of the databases on an instance.

```powershell
# gets the current version of LTR policy for all of the databases on an instance

$Databases = Get-AzSqlInstanceDatabase -ResourceGroupName $resourceGroup -InstanceName $instanceName

$LTRParams = @{
    InstanceName = $instanceName
    ResourceGroupName = $resourceGroup
}

foreach($database in $Databases.Name){
    Get-AzSqlInstanceDatabaseBackupLongTermRetentionPolicy @LTRParams  -DatabaseName $database
 }
```

### Clear an LTR policy

This example shows how to clear an LTR policy from a database.

```powershell
# remove the LTR policy from a database
$LTRPolicy = @{
    InstanceName = $instanceName 
    DatabaseName = $dbName 
    ResourceGroupName = $resourceGroup 
    RemovePolicy = $true
}
Set-AzSqlInstanceDatabaseBackupLongTermRetentionPolicy @LTRPolicy
```

### View LTR backups

This example shows how to list the LTR backups within an instance.

```powershell

$instance = Get-AzSqlInstance -Name $instanceName -ResourceGroupName $resourceGroup

# get the list of all LTR backups in a specific Azure region
# backups are grouped by the logical database id, within each group they are ordered by the timestamp, the earliest backup first
Get-AzSqlInstanceDatabaseLongTermRetentionBackup -Location $instance.Location

# get the list of LTR backups from the Azure region under the given managed instance
$LTRBackupParam = @{
    Location = $instance.Location 
    InstanceName = $instanceName
}
Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam

# get the LTR backups for a specific database from the Azure region under the given managed instance
$LTRBackupParam = @{
    Location = $instance.Location 
    InstanceName = $instanceName
    DatabaseName = $dbName
}
Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam

# list LTR backups only from live databases (you have option to choose All/Live/Deleted)
$LTRBackupParam = @{
    Location = $instance.Location 
    DatabaseState = 'Live'
}
Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam

# only list the latest LTR backup for each database
$LTRBackupParam = @{
    Location = $instance.Location 
    InstanceName = $instanceName
    OnlyLatestPerDatabase = $true
}
Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam 
```

### Delete LTR backups

This example shows how to delete an LTR backup from the list of backups.

```powershell
# remove the earliest backup
# get the LTR backups for a specific database from the Azure region under the given managed instance
$LTRBackupParam = @{
    Location = $instance.Location 
    InstanceName = $instanceName
    DatabaseName = $dbName
}
$ltrBackups = Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam
$ltrBackup = $ltrBackups[0]
Remove-AzSqlInstanceDatabaseLongTermRetentionBackup -ResourceId $ltrBackup.ResourceId
```

> [!IMPORTANT]
> Deleting LTR backup is non-reversible. To delete an LTR backup after the instance has been deleted you must have Subscription scope permission. You can set up notifications about each delete in Azure Monitor by filtering for operation 'Deletes a long term retention backup'. The activity log contains information on who and when made the request. See [Create activity log alerts](/azure/azure-monitor/alerts/alerts-activity-log) for detailed instructions.

### Restore from LTR backups

This example shows how to restore from an LTR backup. Note, this interface did not change but the resource ID parameter now requires the LTR backup resource ID.

```powershell
# restore a specific LTR backup as an P1 database on the instance $instanceName of the resource group $resourceGroup
$LTRBackupParam = @{
    Location = $instance.Location 
    InstanceName = $instanceName
    DatabaseName = $dbname
    OnlyLatestPerDatabase = $true
}
$ltrBackup = Get-AzSqlInstanceDatabaseLongTermRetentionBackup @LTRBackupParam 

$RestoreLTRParam = @{
    TargetInstanceName          = $instanceName 
    TargetResourceGroupName     = $resourceGroup 
    TargetInstanceDatabaseName  = $dbName
    FromLongTermRetentionBackup = $true
    ResourceId                  = $ltrBackup.ResourceId 
}
Restore-AzSqlInstanceDatabase @RestoreLTRParam
```

> [!IMPORTANT]
> To restore from an LTR backup after the instance has been deleted, you must have permissions scoped to the subscription of the instance and that subscription must be active. You must also omit the optional -ResourceGroupName parameter.

> [!NOTE]
> From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name. See [point in time restore](../database/recovery-using-backups.md#point-in-time-restore).

---

## Next steps

- To learn about service-generated automatic backups, see [automatic backups](../database/automated-backups-overview.md)
- To learn about long-term backup retention, see [long-term backup retention](../database/long-term-retention-overview.md)
