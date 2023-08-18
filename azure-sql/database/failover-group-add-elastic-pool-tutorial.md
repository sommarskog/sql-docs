---
title: "Tutorial: Add an elastic pool to a failover group"
description: Add an Azure SQL Database elastic pool to a failover group using the Azure portal, PowerShell, or Azure CLI.
author: rajeshsetlem
ms.author: rsetlem
ms.reviewer: wiassaf, mathoma
ms.date: 01/26/2022
ms.service: sql-database
ms.subservice: high-availability
ms.topic: tutorial
ms.custom: sqldbrb=1, devx-track-azurecli, devx-track-azurepowershell
---
# Tutorial: Add an Azure SQL Database elastic pool to a failover group

[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

> [!div class="op_single_selector"]
>
> - [Azure SQL Database (single database)](failover-group-add-single-database-tutorial.md?view=azuresql-db&preserve-view=true)
> - [Azure SQL Database (elastic pool)](failover-group-add-elastic-pool-tutorial.md?view=azuresql-db&preserve-view=true)
> - [Azure SQL Managed Instance](../managed-instance/failover-group-add-instance-tutorial.md?view=azuresql-mi&preserve-view=true)

Configure an [auto-failover group](auto-failover-group-sql-db.md) for an Azure SQL Database elastic pool and test failover using the Azure portal.

In this tutorial, you'll learn how to:

> [!div class="checklist"]
>
> - Create a single database.
> - Add the database to an elastic pool.
> - Create a failover group for two elastic pools between two servers.
> - Test failover.

## Prerequisites

# [Azure portal](#tab/azure-portal)

To complete this tutorial, make sure you have:

- An Azure subscription. [Create a free account](https://azure.microsoft.com/free/) if you don't already have one.

# [PowerShell](#tab/azure-powershell)

To complete the tutorial, make sure you have the following items:

- An Azure subscription. [Create a free account](https://azure.microsoft.com/free/) if you don't already have one.
- [Azure PowerShell](/powershell/azure/)

# [Azure CLI](#tab/azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]

---

## 1 - Create a single database

In this step, you create a resource group, server, single database, and server-level IP firewall rule for access to the server.

[!INCLUDE [sql-database-create-single-database](../includes/sql-database-create-single-database.md)]

## 2 - Add the database to an elastic pool

In this step, you'll create an elastic pool and add your database to it.

# [Azure portal](#tab/azure-portal)

Create your elastic pool using the Azure portal.

1. Select **Azure SQL** in the left-hand menu of the Azure portal. If **Azure SQL** isn't in the list, select **All services**, then type "Azure SQL" in the search box. (Optional) Select the star next to **Azure SQL** to favorite it and add it as an item in the left-hand navigation.
1. Select **+ Add** to open the **Select SQL deployment option** page. You can view additional information about the different databases by selecting Show details on the Databases tile.
1. Select **Elastic pool** from the **Resource type** drop-down in the **SQL Databases** tile. Select **Create** to create your elastic pool.

    :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/select-azure-sql-elastic-pool.png" alt-text="Screenshot of the Azure portal, deploy Azure SQL resource, with elastic pool selected.":::

1. Configure your elastic pool with the following values:
   - **Name**: Provide a unique name for your elastic pool, such as `myElasticPool`.
   - **Subscription**: Select your subscription from the drop-down.
   - **ResourceGroup**: Select `myResourceGroup` from the drop-down, the resource group you created in section 1.
   - **Server**: Select the server you created in section 1 from the drop-down.  

       :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/use-existing-server-for-elastic-pool.png" alt-text="Screenshot of the create elastic pool page in the Azure portal, with configure elastic pool selected. ":::

   - **Compute + storage**: Select **Configure elastic pool** to configure your compute, storage, and add your single database to your elastic pool. On the **Pool Settings** tab, leave the default of standard-series (Gen5), with 2 vCores and 32 GB of maximum data storage.


1. On the **Configure** page, select the **Databases** tab, and then choose to **Add database**. Choose the database you created in section 1 and then select **Apply** to add it to your elastic pool. Select **Apply** again to apply your elastic pool settings and close the **Configure** page.

    :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/add-database-to-elastic-pool.png" alt-text="Screenshot of the Azure portal, showing where to add databases to the elastic pool.":::

1. Select **Review + create** to review your elastic pool settings and then select **Create** to create your elastic pool.

# [PowerShell](#tab/azure-powershell)

Create your elastic pools and secondary server using PowerShell.

   ```powershell-interactive
   # Set variables for your server and database
   # $subscriptionId = '<SubscriptionID>'
   # $resourceGroupName = "myResourceGroup-$(Get-Random)"
   # $location = "East US"
   # $adminLogin = "azureuser"
   # $password = "PWD27!"+(New-Guid).Guid
   # $serverName = "mysqlserver-$(Get-Random)"
   $poolName = "myElasticPool"
   $databaseName = "mySampleDatabase"
   $drLocation = "West US"
   $drServerName = "mysqlsecondary-$(Get-Random)"
   $failoverGroupName = "failovergrouptutorial-$(Get-Random)"

   # The ip address range that you want to allow to access your server
   # Leaving at 0.0.0.0 will prevent outside-of-azure connections
   # $startIp = "0.0.0.0"
   # $endIp = "0.0.0.0"

   # Show randomized variables
   Write-host "DR Server name is" $drServerName
   Write-host "Failover group name is" $failoverGroupName

   # Create primary standard-series (Gen5) elastic 2 vCore pool
   Write-host "Creating elastic pool..."
   $elasticPool = New-AzSqlElasticPool -ResourceGroupName $resourceGroupName `
       -ServerName $serverName `
       -ElasticPoolName $poolName `
       -Edition "GeneralPurpose" `
       -vCore 2 `
       -ComputeGeneration Gen5
   $elasticPool

   # Add single db into elastic pool
   Write-host "Creating elastic pool..."
   $addDatabase = Set-AzSqlDatabase -ResourceGroupName $resourceGroupName `
       -ServerName $serverName `
       -DatabaseName $databaseName `
       -ElasticPoolName $poolName
   $addDatabase
   ```

This portion of the tutorial uses the following PowerShell cmdlets:

| Command | Notes |
|---|---|
| [New-AzSqlElasticPool](/powershell/module/az.sql/new-azsqlelasticpool) | Creates an elastic database pool for an Azure SQL Database.|
| [Set-AzSqlDatabase](/powershell/module/az.sql/set-azsqldatabase) | Sets properties for a database, or moves an existing database into an elastic pool. |

# [Azure CLI](#tab/azure-cli)

In this step, you create your elastic pool and add your database to the elastic pool using the Azure CLI.

### Set additional parameter values to create elastic pool

Set these additional parameter values for use in creating the elastic pool.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="SetPoolParameterValues":::

### Create elastic pool on primary server

Use the [az sql elastic-pool create](/cli/azure/sql/elastic-pool#az-sql-elastic-pool-create) command to create an elastic pool.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="CreateElasticPool":::

### Add database to elastic pool

Use the [az sql db update](/cli/azure/sql/db#az-sql-db-update) command to add a database to an elastic pool.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="AddDatabaseToPool":::

This portion of the tutorial uses the following Azure CLI cmdlets:

| Command | Notes |
|---|---|
| [az sql elastic-pool create](/cli/azure/sql/elastic-pool#az-sql-elastic-pool-create) | Creates an elastic pool. |
| [az sql db update](/cli/azure/sql/db#az-sql-db-update) | Updates a database|

---

## 3 - Create the failover group

In this step, you'll create a [failover group](auto-failover-group-sql-db.md) between an existing server and a new server in another region. Then add the elastic pool to the failover group.

# [Azure portal](#tab/azure-portal)

Create your failover group using the Azure portal.

1. Select **Azure SQL** in the left-hand menu of the [Azure portal](https://portal.azure.com). If **Azure SQL** isn't in the list, select **All services**, then type Azure SQL in the search box. (Optional) Select the star next to **Azure SQL** to favorite it and add it as an item in the left-hand navigation.
1. Select the elastic pool created in the previous section, such as `myElasticPool`.
1. On the **Overview** pane, select the name of the server under **Server name** to open the settings for the server.
  
    :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/server-for-elastic-pool.png" alt-text="Screenshot of the Azure portal, elastic pool overview page, selecting the server name. ":::

1. Select **Failover groups** under the **Settings** pane, and then select **Add group** to create a new failover group.

    :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/elastic-pool-failover-group.png" alt-text="Screenshot of the logical server in Azure, showing to add a new failover group on the failover group page.":::

1. On the **Failover Group** page, enter or select the following values, and then select **Create**:
    - **Failover group name**: Type in a unique failover group name, such as `failovergrouptutorial`.
    - **Secondary server**: Select the option to *configure required settings* and then choose to **Create a new server**. Alternatively, you can choose an already-existing server as the secondary server. After entering the following values for your new secondary server, select **Select**.
        - **Server name**: Type in a unique name for the secondary server, such as `mysqlsecondary`.
        - **Server admin login**: Type `azureuser`
        - **Password**: Type a complex password that meets password requirements.
        - **Location**: Choose a location from the drop-down, such as `East US`. This location can't be the same location as your primary server.

       > [!NOTE]
       > The server login and firewall settings must match that of your primary server.

       :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/create-secondary-failover-server.png" alt-text="Screenshot of the Azure portal showing to create a secondary server for the failover group.":::

1. Select **Databases within the group** then select the elastic pool you created in section 2. A warning should appear, prompting you to create an elastic pool on the secondary server. Select the warning, and then select **OK** to create the elastic pool on the secondary server.

   :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/add-elastic-pool-to-failover-group.png" alt-text="Screenshot of the Azure portal, showing how to add elastic pool to the failover group.":::

1. Select **Select** to apply your elastic pool settings to the failover group, and then select **Create** to create your failover group. Adding the elastic pool to the failover group will automatically start the geo-replication process.

# [PowerShell](#tab/azure-powershell)

Create your failover group using PowerShell.

   ```powershell-interactive
   # Set variables for your server and database
   # $subscriptionId = '<SubscriptionID>'
   # $resourceGroupName = "myResourceGroup-$(Get-Random)"
   # $location = "East US"
   # $adminLogin = "azureuser"
   # $password = "PWD27!"+(New-Guid).Guid
   # $serverName = "mysqlserver-$(Get-Random)"
   # $poolName = "myElasticPool"
   # $databaseName = "mySampleDatabase"
   # $drLocation = "West US"
   # $drServerName = "mysqlsecondary-$(Get-Random)"
   $failoverGroupName = "failovergrouptutorial-$(Get-Random)"

   # Create a secondary server in the failover region
   Write-host "Creating a secondary server in the failover region..."
   New-AzSqlServer -ResourceGroupName $resourceGroupName `
      -ServerName $drServerName `
      -Location $drLocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential `
         -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   Write-host "Secondary server =" $drServerName

   # Create a server firewall rule that allows access from the specified IP range
   Write-host "Configuring firewall for secondary server..."
   New-AzSqlServerFirewallRule -ResourceGroupName $resourceGroupName `
      -ServerName $drServerName `
      -FirewallRuleName "AllowedIPs" -StartIpAddress $startIp -EndIpAddress $endIp
   Write-host "Firewall configured"

   # Create secondary standard-series (Gen5) elastic 2 vCore pool
   Write-host "Creating secondary elastic pool..."
   $elasticPool = New-AzSqlElasticPool -ResourceGroupName $resourceGroupName `
       -ServerName $drServerName `
       -ElasticPoolName $poolName `
       -Edition "GeneralPurpose" `
       -vCore 2 `
       -ComputeGeneration Gen5
   $elasticPool

   # Create a failover group between the servers
   Write-host "Creating failover group..."
   New-AzSqlDatabaseFailoverGroup `
     ResourceGroupName $resourceGroupName `
      -ServerName $serverName `
      -PartnerServerName $drServerName  `
      FailoverGroupName $failoverGroupName `
      FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   Write-host "Failover group created successfully."

   # Add elastic pool to the failover group
   Write-host "Enumerating databases in elastic pool...."
   $FailoverGroup = Get-AzSqlDatabaseFailoverGroup `
                    -ResourceGroupName $resourceGroupName `
                    -ServerName $serverName `
                    -FailoverGroupName $failoverGroupName
   $databases = Get-AzSqlElasticPoolDatabase `
                  -ResourceGroupName $resourceGroupName `
                  -ServerName $serverName `
                  -ElasticPoolName $poolName
   Write-host "Adding databases to failover group..."
   $failoverGroup = $failoverGroup | Add-AzSqlDatabaseToFailoverGroup `
                                     -Database $databases
   $failoverGroup
   ```

This portion of the tutorial uses the following PowerShell cmdlets:

| Command | Notes |
|---|---|
| [New-AzSqlServer](/powershell/module/az.sql/new-azsqlserver) | Creates a server that hosts databases and elastic pools. |
| [New-AzSqlServerFirewallRule](/powershell/module/az.sql/new-azsqlserverfirewallrule) | Creates a firewall rule for a server. |
| [New-AzSqlElasticPool](/powershell/module/az.sql/new-azsqlelasticpool) | Creates an elastic pool for an Azure SQL Database.|
| [New-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/new-azsqldatabasefailovergroup) | Creates a new failover group. |
| [Add-AzSqlDatabaseToFailoverGroup](/powershell/module/az.sql/add-azsqldatabasetofailovergroup) | Adds one or more Azure SQL databases to a failover group. |
| [Get-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/get-azsqldatabasefailovergroup) | Gets or lists Azure SQL Database failover groups. |

# [Azure CLI](#tab/azure-cli)

In this step, you use the Azure CLI to create your secondary server, failover group, elastic pool, and add a database to the failover group.

### Set additional parameter values to create failover group

Set these additional parameter values for use in creating the failover group.

Change the failover location as appropriate for your environment.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="SetFailoverParameterValues":::

### Create secondary server

Use the [az sql server create](/cli/azure/sql/server#az-sql-server-create) command to create a secondary server.
> [!NOTE]
> The server login and firewall settings must match that of your primary server.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="CreateSecondaryServer":::

### Create elastic pool on secondary server

Use the [az sql elastic-pool create](/cli/azure/sql/elastic-pool#az-sql-elastic-pool-create) command to create an elastic pool on the secondary server.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="CreateElasticPoolOnSecondary":::

### Create failover group

Use the [az sql failover-group create](/cli/azure/sql/failover-group#az-sql-failover-group-create) command to create a failover group.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="CreateFailoverGroup":::

### Add database to the failover group

Use the [az sql failover-group update](/cli/azure/sql/failover-group#az-sql-failover-group-update) command to add a database to the failover group.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="AddDatabaseToFailoverGroup":::

### Azure CLI failover group creation reference

This portion of the tutorial uses the following Azure CLI cmdlets:

| Command | Notes |
|---|---|
| [az sql server create](/cli/azure/sql/server#az-sql-server-create) | Creates a server that hosts databases and elastic pools. |
| [az sql elastic-pool create](/cli/azure/sql/elastic-pool#az-sql-elastic-pool-create) | Creates an elastic pool.|
| [az sql failover-group create](/cli/azure/sql/failover-group#az-sql-failover-group-create) | Creates a failover group. |
| [az sql failover-group update](/cli/azure/sql/failover-group#az-sql-failover-group-update) | Updates a failover group.|

---

## 4 - Test failover

In this step, you'll fail your failover group over to the secondary server, and then fail back using the Azure portal.

# [Azure portal](#tab/azure-portal)

Test failover of your failover group using the Azure portal.

1. Select **Azure SQL** in the left-hand menu of the [Azure portal](https://portal.azure.com). If **Azure SQL** isn't in the list, select **All services**, then type Azure SQL in the search box. (Optional) Select the star next to **Azure SQL** to favorite it and add it as an item in the left-hand navigation.
1. Select the elastic pool created in the previous section, such as `myElasticPool`.
1. Select the name of the server under **Server name** to open the settings for the server.

    :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/server-for-elastic-pool.png" alt-text="Screenshot of the elastic pool overview page selecting the server name.":::

1. Select **Failover groups** under the **Settings** pane and then choose the failover group you created in section 2.
  
   :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/select-failover-group.png" alt-text="Screenshot of the Azure portal for the logical server, selecting the existing failover group. ":::

1. Review which server is primary, and which server is secondary.
1. Select **Failover** from the task pane to fail over your failover group containing your elastic pool.
1. Select **Yes** on the warning that notifies you that TDS sessions will be disconnected.

   :::image type="content" source="./media/failover-group-add-elastic-pool-tutorial/failover-sql-db.png" alt-text="Screenshot of the Failover group for your elastic pool, with failover selected. ":::

1. Review which server is primary, which server is secondary. If failover succeeded, the two servers should have swapped roles.
1. Select **Failover** again to fail the failover group back to the original settings.

# [PowerShell](#tab/azure-powershell)

Test failover of your failover group using PowerShell.

   ```powershell-interactive
   # Set variables for your server and database
   # $subscriptionId = '<SubscriptionID>'
   # $resourceGroupName = "myResourceGroup-$(Get-Random)"
   # $location = "East US"
   # $adminLogin = "azureuser"
   # $password = "PWD27!"+(New-Guid).Guid
   # $serverName = "mysqlserver-$(Get-Random)"
   # $poolName = "myElasticPool"
   # $databaseName = "mySampleDatabase"
   # $drLocation = "West US"
   # $drServerName = "mysqlsecondary-$(Get-Random)"
   # $failoverGroupName = "failovergrouptutorial-$(Get-Random)"

   # Check role of secondary replica
   Write-host "Confirming the secondary server is secondary...."
   (Get-AzSqlDatabaseFailoverGroup `
      -FailoverGroupName $failoverGroupName `
      -ResourceGroupName $resourceGroupName `
      -ServerName $drServerName).ReplicationRole

   # Failover to secondary server
   Write-host "Failing over failover group to the secondary..."
   Switch-AzSqlDatabaseFailoverGroup `
      -ResourceGroupName $resourceGroupName `
      -ServerName $drServerName `
      -FailoverGroupName $failoverGroupName
   Write-host "Failover group failed over to" $drServerName
   ```

Fail your failover group over to the secondary server, and then fail back using the PowerShell.

   ```powershell-interactive
   # Set variables for your server and database
   # $subscriptionId = '<SubscriptionID>'
   # $resourceGroupName = "myResourceGroup-$(Get-Random)"
   # $location = "East US"
   # $adminLogin = "azureuser"
   # $password = "PWD27!"+(New-Guid).Guid
   # $serverName = "mysqlserver-$(Get-Random)"
   # $poolName = "myElasticPool"
   # $databaseName = "mySampleDatabase"
   # $drLocation = "West US"
   # $drServerName = "mysqlsecondary-$(Get-Random)"
   # $failoverGroupName = "failovergrouptutorial-$(Get-Random)"

   # Check role of secondary replica
   Write-host "Confirming the secondary server is now primary"
   (Get-AzSqlDatabaseFailoverGroup `
      -FailoverGroupName $failoverGroupName `
      -ResourceGroupName $resourceGroupName `
      -ServerName $drServerName).ReplicationRole

   # Revert failover to primary server
   Write-host "Failing over failover group to the primary...."
   Switch-AzSqlDatabaseFailoverGroup `
      -ResourceGroupName $resourceGroupName `
      -ServerName $serverName `
      -FailoverGroupName $failoverGroupName
   Write-host "Failover group failed over to" $serverName
   ```

This portion of the tutorial uses the following PowerShell cmdlets:

| Command | Notes |
|---|---|
| [Get-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/get-azsqldatabasefailovergroup) | Gets or lists Azure SQL Database failover groups. |
| [Switch-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/switch-azsqldatabasefailovergroup)| Executes a failover of an Azure SQL Database failover group. |

# [Azure CLI](#tab/azure-cli)

Test failover using the Azure CLI.

### Verify the roles of each server

Use the [az sql failover-group show](/cli/azure/sql/failover-group#az-sql-failover-group-show) command to confirm the roles of each server in the failover group.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="VerifyRoles":::

### Fail over to the secondary server

Use the [az sql failover-group set-primary](/cli/azure/sql/failover-group#az-sql-failover-group-set-primary) command to fail over to the secondary server. Use the [az sql failover-group show](/cli/azure/sql/failover-group#az-sql-failover-group-show) command to verify a successful failover.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="FailingOver":::

### Revert failover group back to the primary server

Use the [az sql failover-group set-primary](/cli/azure/sql/failover-group#az-sql-failover-group-set-primary) command to fail back to the primary server.

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="FailingBack":::

### Azure CLI failover group management reference

This portion of the tutorial uses the following Azure CLI cmdlets:

| Command | Notes |
|---|---|
| [az sql failover-group show](/cli/azure/sql/failover-group#az-sql-failover-group-show) | Gets the failover groups in a server. |
| [az sql failover-group set-primary](/cli/azure/sql/failover-group#az-sql-failover-group-set-primary) | Set the primary of the failover group by failing over all databases from the current primary server. |

---

## Clean up resources

Clean up resources by deleting the resource group.

# [Azure portal](#tab/azure-portal)

1. Navigate to your resource group in the [Azure portal](https://portal.azure.com).
1. Select  **Delete resource group** to delete all the resources in the group, as well as the resource group itself.
1. Type the name of the resource group, `myResourceGroup`, in the textbox, and then select **Delete** to delete the resource group.

# [PowerShell](#tab/azure-powershell)

Clean up your resources using PowerShell.

   ```powershell-interactive
   # Set variables for your server and database
   # $resourceGroupName = "myResourceGroup-$(Get-Random)"

   # Clean up resources by removing the resource group
   Write-host "Removing resource group..."
   Remove-AzResourceGroup -ResourceGroupName $resourceGroupName
   Write-host "Resource group removed =" $resourceGroupName
   ```

This portion of the tutorial uses the following PowerShell cmdlet:

| Command | Notes |
|---|---|
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Removes a resource group |

# [Azure CLI](#tab/azure-cli)

[!INCLUDE [cli-clean-up-resources.md](../includes/cli-clean-up-resources.md)]

   ```azurecli
   echo "Cleaning up resources by removing the resource group..."
   az group delete --name $resourceGroup -y
   ```

This portion of the tutorial uses the following Azure CLI cmdlets:

| Command | Notes |
|---|---|
| [az group delete](/cli/azure/vm/extension#az-vm-extension-set) | Deletes a resource group including all nested resources. |

---

> [!IMPORTANT]
> If you want to keep the resource group but delete the secondary database, remove it from the failover group before deleting it. Deleting a secondary database before it is removed from the failover group can cause unpredictable behavior.

## Full script

# [PowerShell](#tab/azure-powershell)

[!code-powershell-interactive[main](~/../powershell_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-ps.ps1 "Add elastic pool to a failover group")]

This script uses the following commands. Each command in the table links to command specific documentation.

| Command | Notes |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | Creates a resource group in which all resources are stored. |
| [New-AzSqlServer](/powershell/module/az.sql/new-azsqlserver) | Creates a server that hosts databases and elastic pools. |
| [New-AzSqlServerFirewallRule](/powershell/module/az.sql/new-azsqlserverfirewallrule) | Creates a firewall rule for a server. |
| [New-AzSqlDatabase](/powershell/module/az.sql/new-azsqldatabase) | Creates a database. |
| [New-AzSqlElasticPool](/powershell/module/az.sql/new-azsqlelasticpool) | Creates an elastic database pool for an Azure SQL Database.|
| [Set-AzSqlDatabase](/powershell/module/az.sql/set-azsqldatabase) | Sets properties for a database, or moves an existing database into an elastic pool. |
| [New-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/new-azsqldatabasefailovergroup) | Creates a new failover group. |
| [Get-AzSqlDatabase](/powershell/module/az.sql/get-azsqldatabase) | Gets one or more databases in SQL Database. |
| [Add-AzSqlDatabaseToFailoverGroup](/powershell/module/az.sql/add-azsqldatabasetofailovergroup) | Adds one or more Azure SQL databases to a failover group. |
| [Get-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/get-azsqldatabasefailovergroup) | Gets or lists Azure SQL Database failover groups. |
| [Switch-AzSqlDatabaseFailoverGroup](/powershell/module/az.sql/switch-azsqldatabasefailovergroup)| Executes a failover of an Azure SQL Database failover group. |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Removes a resource group |

# [Azure CLI](#tab/azure-cli)

:::code language="azurecli" source="~/../azure_cli_scripts/sql-database/failover-groups/add-elastic-pool-to-failover-group-az-cli.sh" id="FullScript":::

# [Azure portal](#tab/azure-portal)

There are no scripts available for the Azure portal.

---

## Next steps

In this tutorial, you added an Azure SQL Database elastic pool to a failover group, and tested failover. You learned how to:

> [!div class="checklist"]
>
> - Create a single database.
> - Add the database into an elastic pool.
> - Create a [failover group](auto-failover-group-sql-db.md) for two elastic pools between two servers.
> - Test failover.

Advance to the next tutorial on how to migrate using DMS.

> [!div class="nextstepaction"]
> [Tutorial: Migrate SQL Server to a pooled database using DMS](/azure/dms/tutorial-sql-server-to-azure-sql?toc=/azure/sql-database/toc.json)
