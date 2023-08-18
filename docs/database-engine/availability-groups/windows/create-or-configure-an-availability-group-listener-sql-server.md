---
title: "Configure availability group listener"
description: "Describes the steps to take when configuring a listener for an Always On availability group using PowerShell or SQL Server Management Studio. "
author: MashaMSFT
ms.author: mathoma
ms.date: "05/17/2016"
ms.service: sql
ms.subservice: availability-groups
ms.topic: how-to
f1_keywords:
  - "sql13.swb.availabilitygroup.newaglistener.general.f1"
helpviewer_keywords:
  - "Availability Groups [SQL Server], listeners"
  - "Availability Groups [SQL Server], client connectivity"
---
# Configure a listener for an Always On availability group
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to create or configure a single *availability group listener* for an Always On availability group by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], or PowerShell in [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  To create the first availability group listener of an availability group, we strongly recommend that you use [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], or [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Avoid creating a listener directly in the WSFC cluster except when necessary, for example, to create an additional listener.  
  
 
##  <a name="DoesListenerExist"></a> Does a Listener Exist for this Availability Group Already?  

 **To determine whether a listener already exists for the availability group**  
  
-   [View Availability Group Listener Properties &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
> [!NOTE]  
>  If a listener already exists and you want to create an additional listener, see [To Create An Additional Listener for an Availability Group (Optional)](#CreateAdditionalListener), later in this topic.  
  
##  <a name="Restrictions"></a> Limitations and Restrictions  
  
-   You can create only one listener per availability group through [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Typically, each availability group requires only one listener. However, some customer scenarios require multiple listeners for one availability group.   After creating a listener through SQL Server, you can use Windows PowerShell for failover clusters or the WSFC Failover Cluster Manager to create additional listeners. For more information, see [To Create An Additional Listener for an Availability Group (Optional)](#CreateAdditionalListener), later in this topic.  
  
##  <a name="Recommendations"></a> Recommendations  
 Using a static IP address is recommended, although not required, for multiple subnet configurations.  
  
##  <a name="Prerequisites"></a> Prerequisites  
  
-   You must be connected to the server instance that hosts the primary replica.  
  
-   If you are setting up an availability group listener across multiple subnets and plan to use static IP addresses, you need to get the static IP address of every subnet that hosts an availability replica for the availability group for which you are creating the listener. Usually, you will need to ask your network administrators for the static IP addresses.  
  
> [!IMPORTANT]  
>  Before you create your first listener, we strongly recommend that you read [Always On Client Connectivity &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="DNSnameReqs"></a> Requirements for the DNS Name of an Availability Group Listener  
 Each availability group listener requires a DNS host name that is unique in the domain and in NetBIOS. The DNS name is a string value. This name can contain only alphanumeric characters, dashes/hyphens (-), and underscores (_), in any order. DNS host names are case insensitive. The maximum length is 63 characters, however, in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], the maximum length you can specify is 15 characters.  
  
 We recommend that you specify a meaningful string. For example, for an availability group named `AG1`, a meaningful DNS host name would be `ag1-listener`.  
  
> [!IMPORTANT]  
>  NetBIOS recognizes only the first 15 chars in the dns_name. If you have two WSFC clusters that are controlled by the same Active Directory and you try to create availability group listeners in both of clusters using names with more than 15 characters and an identical 15 character prefix, you will get an error reporting that the Virtual Network Name resource could not be brought online. For information about prefix naming rules for DNS names, see [Assigning Domain Names](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
##  <a name="WinPermissions"></a> Windows Permissions  
  
|Permissions|Link|  
|-----------------|----------|  
|The cluster name object (CNO) of WSFC cluster that is hosting the availability group must have **Create Computer objects** permission.<br /><br /> In Active Directory, a CNO by default does not have **Create Computer objects** permission explicitly and can create 10 virtual computer objects (VCOs). After 10 VCOs are created, the creation of additional VCOs will fail. You can avoid this by granting the permission explicitly to the WSFC cluster's CNO. Note that VCOs for availability groups that you have deleted are not automatically deleted in Active Directory and count against your 10 VCO default limit unless they are manually deleted.<br /><br /> Note: In some organizations, the security policy prohibits granting **Create Computer objects** permission to individual user accounts.|*Steps for configuring the account for the person who installs the cluster* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002(v=ws.10)#BKMK_steps_installer)<br /><br /> *Steps for prestaging the cluster name account* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002(v=ws.10)#BKMK_steps_precreating)|  
|If your organization requires that you prestage the computer account for a listener virtual network name, you will need membership in the **Account Operator** group or your domain administrator's assistance.|*Steps for prestaging an account for a clustered service or application* in [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002(v=ws.10)#BKMK_steps_precreating2).|  
  
> [!TIP]  
>  Generally, it is simplest not to prestage the computer account for a listener virtual network name. If you can, let the account to be created and configured automatically when you run the WSFC High Availability wizard.  
  
##  <a name="SqlPermissions"></a> SQL Server Permissions  
  
|Task|Permissions|  
|----------|-----------------|  
|To create an availability group listener|Requires membership in the **sysadmin** fixed server role and either CREATE AVAILABILITY GROUP server permission, ALTER ANY AVAILABILITY GROUP permission, or CONTROL SERVER permission.|  
|To modify an existing availability group listener|Requires ALTER AVAILABILITY GROUP permission on the availability group, CONTROL AVAILABILITY GROUP permission, ALTER ANY AVAILABILITY GROUP permission, or CONTROL SERVER permission.|  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
> [!TIP]  
>  The [New Availability Group wizard](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) supports creation of the listener for a new availability group.  
  
 **To create or configure an availability group listener**  
  
1.  In Object Explorer, connect to the server instance that hosts the primary replica of the availability group, and click the server name to expand the server tree.  
  
2.  Expand the **Always On High Availability** node and the **Availability Groups** node.  
  
3.  Click the availability group whose listener you want to configure, and choose one of the following alternatives:  
  
    -   To create a listener, right-click the **Availability group Listeners** node, and select the **New Listener** command. This opens the **New Availability Group Listener** dialog box. For more information, see [Add Availability Group Listener (Dialog Box)](#AddAgListenerDialog), later in this topic.  
  
    -   To change the port number of an existing listener, expand the **Availability group Listeners** node, right-click the listener, and select the **Properties** command. Enter the new port number into the **Port** field, and click **OK**.  
  
###  <a name="AddAgListenerDialog"></a> New Availability Group Listener (Dialog Box)  
 **Listener DNS Name**  
 Specifies the DNS host name of the availability group listener. The DNS name is a string  must be unique in the domain and in NetBIOS. This name can contain only alphanumeric characters, dashes (-), and hyphens (_), in any order. DNS host names are case insensitive. The maximum length is 15 characters.  
  
 For more information, see [Requirements for the DNS Name of an Availability Group Listener](#DNSnameReqs), earlier in this topic.  
  
 **Port**  
 The TCP port used by this listener.  
  
 **Network Mode**  
 Indicates the TCP protocol used by the listener, one of:  
  
 **DHCP**  
 The listener will us a dynamic IP address that is assigned by a server running the Dynamic Host Configuration Protocol (DHCP). DHCP is limited to a single subnet.  
  
> [!IMPORTANT]  
>  We do not recommend DHCP in production environment. If there is a down time and the DHCP IP lease expires, extra time is required to register the new DHCP network IP address that is associated with the listener DNS name and impact the client connectivity. However, DHCP is good for setting up your development and testing environment to verify basic functions of availability groups and for integration with your applications.  
  
 **Static IP**  
 The listener will use one or more static IP addresses. Additional IP addresses are optional. To create an availability group listener across multiple subnets, for each subnet you must specify a static IP address in the listener configuration. Contact your network administrator to get these static IP addresses.  
  
 If you select **Static IP** a subnet grid appears below the **Network Mode** field. This grid displays information about each subnet that can be accessed by this availability group listener. This grid is empty until you add a static IP address by clicking **Add**.  
  
 The columns are as follows:  
  
 **Subnet**  
 Displays the identifier of each subnet that you add to the availability group listener.  
  
 **IP Address**  
 Displays the IP address of a given subnet.  For a given subnet, the IP address is either an IPv4 address or an IPv6 address.  
  
 **Add**  
 Click to add to add a static IP address to a selected subnet or to another subnet for this listener. This opens the **Add IP Address** dialog box. For more information, see the [Add IP Address Dialog Box &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md) help topic.  
  
 **Remove**  
 Click to remove the selected subnet from this listener.  
  
 **OK**  
 Click to create the specified availability group listener.  
  
##  <a name="TsqlProcedure"></a> Using Transact-SQL  
 **To create or configure an availability group listener**  
  
1.  Connect to the server instance that hosts the primary replica.  
  
2.  Use the LISTENER option of the [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) statement or the ADD LISTENER option of the [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) statement.  
  
     The following example adds an availability group listener to an existing availability group named `MyAg2`. A unique DNS name, `MyAg2ListenerIvP6`, is specified for this listener. The two replicas are on different subnets, so , as recommended, the listener uses static IP addresses. For each of the two availability replicas, the WITH IP clause specifies a static IP address, `2001:4898:f0:f00f::cf3c and 2001:4898:e0:f213::4ce2`, which use the IPv6 format. This example also specifies uses the optional PORT argument to specify port `60173` as the listener port.  
  
    ```sql  
    ALTER AVAILABILITY GROUP MyAg2   
          ADD LISTENER 'MyAg2ListenerIvP6' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a> Using PowerShell  
 **To create or configure an availability group listener**  
  
1.  Change directory (**cd**) to the server instance that hosts the primary replica.  
  
2.  To create or modify an availability group listener use one of the following cmdlets:  
  
     **New-SqlAvailabilityGroupListener**  
     Creates a new availability group listener and attaches it to an existing availability group.  
  
     For example, the following **New-SqlAvailabilityGroupListener** command creates an availability group listener named `MyListener` for the availability group `MyAg`. This listener will use the IPv4 address passed to the **-StaticIp** parameter as its virtual IP address.  
  
    ```powershell  
    New-SqlAvailabilityGroupListener -Name MyListener `   
    -StaticIp '192.168.3.1/255.255.252.0' `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
  
    ```  
  
     **Set-SqlAvailabilityGroupListener**  
     Modifies the port setting on an existing availability group listener.  
  
     For example, the following **Set-SqlAvailabilityGroupListener** command sets the port number for the availability group listener named `MyListener` to `1535`. This port is used to listen for connections to the listener.  
  
    ```powershell  
    Set-SqlAvailabilityGroupListener -Port 1535 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
  
    ```  
  
     **Add-SqlAGListenerstaticIp**  
     Adds a static IP address to an existing availability group listener configuration. The IP address can be an IPv4 address with subnet, or an IPv6 address.  
  
     For example, the following **Add-SqlAGListenerstaticIp** command adds a static IPv4 address to the availability group listener `MyListener` on the availability group `MyAg`. This IPv6 address serves as the virtual IP address of the listener on the subnet `255.255.252.0`. If the availability group spans multiple subnets, you should add a static IP address for each subnet to the listener.  
  
    ```powershell
    $path = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\ MyListener" `   
    Add-SqlAGListenerstaticIp -Path $path `   
    -StaticIp "2001:0db8:85a3:0000:0000:8a2e:0370:7334"  
    ```  
  
    > [!NOTE]  
    >  To view the syntax of a cmdlet, use the **Get-Help**  cmdlet in the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell environment. For more information, see [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **To set up and use the SQL Server PowerShell provider**  
  
-   [SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
## Troubleshooting  
  
###  <a name="ADQuotas"></a> Failure to Create An Availability Group Listener Because of Active Directory Quotas  
 The creation of a new availability group listener may fail upon creation because you have reached an Active Directory quota for the participating cluster node machine account.  For more information, see the following articles:  
  
-   [How to Troubleshoot the Cluster Service Account When It Modifies Computer Objects](https://support.microsoft.com/kb/307532)  
  
-   [Active Directory Quotas](https://technet.microsoft.com/library/cc904295\(WS.10\).aspx)  
  
##  <a name="FollowUp"></a> Follow-up: After Creating an Availability Group Listener  
  
###  <a name="MultiSubnetFailover"></a> MultiSubnetFailover Keyword and Associated Features  
 **MultiSubnetFailover** is a new connection string keyword used to enable faster failover with Always On Availability Groups and Always On Failover Cluster Instances in SQL Server 2012. The following three sub-features are enabled when `MultiSubnetFailover=True` is set in connection string:  
  
-   Faster multi-subnet failover to a multi-subnet listener for an Always On Availability Group or Failover Cluster Instances.  
  
-   Faster single subnet failover to a single subnet listener for an Always On Availability Group or Failover Cluster Instances.  
  
    -   This feature is used when connecting to a listener that has a single IP in a single subnet. This performs more aggressive TCP connection retries to speed up single subnet failovers.  
  
-   Named instance resolution to a multi-subnet Always On Failover Cluster Instance.  
  
    -   This is to add named instance resolution support for an Always On Failover Cluster Instances with multiple subnet endpoints.  
  
 **MultiSubnetFailover=True Not Supported by NET Framework 3.5 or OLEDB**  
  
 **Issue:** If your Availability Group or Failover Cluster Instance has a listener name (known as the network name or Client Access Point in the WSFC Cluster Manager) depending on multiple IP addresses from different subnets, and you are using either ADO.NET with .NET Framework 3.5SP1 or SQL Native Client 11.0 OLEDB, potentially 50% of your client-connection requests to the availability group listener will hit a connection timeout.  
  
 **Workarounds:** We recommend that you do one of the following tasks.  
  
-   If do not have the permission to manipulate cluster resources, change your connection timeout to 30 seconds (this value results in a 20-second TCP timeout period plus a 10-second buffer).  
  
     **Pros**: If a cross-subnet failover occurs, client recovery time is short.  
  
     **Cons**: Half of the client connections will take more than 20 seconds  
  
-   If you have the permission to manipulate cluster resources, the more recommended approach is to set the network name of your availability group listener to `RegisterAllProvidersIP=0`. For more information, see "RegisterAllProvidersIP Setting" later in this section.  
  
     **Pros:** You do not need to increase your client-connection timeout value.  
  
     **Cons:** If a cross-subnet failover occurs, the client recovery time could be 15 minutes or longer, depending on your **HostRecordTTL** setting and the setting of your cross-site DNS/AD replication schedule.  
  
###  <a name="RegisterAllProvidersIP"></a> RegisterAllProvidersIP Setting  
 When you use [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], or PowerShell to create an availability group listener, the Client Access Point is created in WSFC with the **RegisterAllProvidersIP** property set to 1 (true). The effect of this property value depends on the client connection string, as follows:  
  
-   Connection strings that set **MultiSubnetFailover** to true  
  
     [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sets the  **RegisterAllProvidersIP** property to 1 in order to reduce re-connection time after a failover for clients whose client connection strings specify `MultiSubnetFailover = True`, as recommended. Note that to take advantage of the listener multi-subnet feature, your clients might require a data provider that supports the **MultiSubnetFailover** keyword. For information about driver support for multi-subnet failover, see [Always On Client Connectivity &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
     For information about multi-subnet clustering, see [SQL Server Multi-Subnet Clustering &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
    > [!TIP]  
    >  When `RegisterAllProvidersIP = 1`, if you run the WSFC Validate a Configuration Wizard on the WSFC cluster, the wizard generates the following warning message:  
    >   
    >  "The RegisterAllProviderIP property for network name 'Name:<network_name>' is set to 1 For the current cluster configuration this value should be set to 0."  
    >   
    >  Please ignore this message.  
  
-   Connection strings that do not set **MultiSubnetFailover** to true  
  
     When `RegisterAllProvidersIP = 1`, any clients whose connection strings do not use `MultiSubnetFailover = True`, will experience high latency connections. This occurs because these clients attempt connections to all IPs sequentially. In contrast, if **RegisterAllProvidersIP** is changed to 0, the active IP address is registered in the Client Access Point in the WSFC cluster, reducing latency for legacy clients. Therefore, if you have legacy clients that need to connect to an availability group listener and cannot use the **MultiSubnetFailover** property, we recommend that you change **RegisterAllProvidersIP** to 0.  
  
    > [!IMPORTANT]  
    >  When you create an availability group listener through the WSFC cluster (Failover Cluster Manager GUI), **RegisterAllProvidersIP** will be 0 (false) by default.  
  
###  <a name="HostRecordTTL"></a> HostRecordTTL Setting  
 By default, clients cache cluster DNS records for 20 minutes.  By reducing **HostRecordTTL**, the Time to Live (TTL), for the cached record, legacy clients may reconnect more quickly.  However, reducing the **HostRecordTTL** setting may also result in increased traffic to the DNS servers.  
  
###  <a name="SampleScript"></a> Sample PowerShell Script to Disable RegisterAllProvidersIP and Reduce TTL  
 The following PowerShell example demonstrates how to configure both the **RegisterAllProvidersIP** and **HostRecordTTL** cluster parameters for the listener resource.  The DNS record will be cached for 5 minutes rather than the default 20 minutes.  Modifying both cluster parameters may reduce the time to connect to the correct IP address after a failover for legacy clients that cannot use the **MultiSubnetFailover** parameter.  Replace `yourListenerName` with the name of the listener that you are changing.  
  
```powershell  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName | Set-ClusterParameter RegisterAllProvidersIP 0   
Get-ClusterResource yourListenerName | Set-ClusterParameter HostRecordTTL 300  
Stop-ClusterResource yourListenerName  
Start-ClusterResource yourListenerName  
Start-Clustergroup yourListenerGroupName
```  
  
 For more information about recovery times during failover, see [Client Recovery Latency During Failover](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md#DNS).  
  
###  <a name="FollowUpRecommendations"></a> Follow-up Recommendations  
 After you create an availability group listener:  
  
-   Ask your network administrator to reserve the listener's IP address for its exclusive use.  
  
-   Give the listener's DNS host name to application developers to use in connection strings when requesting client connections to this availability group.  
  
-   Encourage developers to update client connection strings to specify `MultiSubnetFailover = True`, if possible. For information about driver support for multi-subnet failover, see [Always On Client Connectivity &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="CreateAdditionalListener"></a> Create an Additional Listener for an Availability Group (Optional)  
 After you create one listener through SQL Server, you can add an additional listener, as follows:  
  
1.  Create the listener using either of the following tools:  
  
    -   **Using WSFC Failover Cluster Manager:**  
  
        1.  Add a client access point and configure the IP address.  
  
        2.  Bring the listener online.  
  
        3.  Add a dependency to the WSFC availability group resource.  
  
         For information about the dialog boxes and tabs of the Failover Cluster Manager, see [User Interface: The Failover Cluster Manager Snap-In](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772502(v=ws.11)).  
  
    -   **Using Windows PowerShell for failover clusters:**  
  
        1.  Use [Add-ClusterResource](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee460983(v=technet.10)) to create a network name and the IP address resources.  
  
        2.  Use [Start-ClusterResource](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461056(v=technet.10)) to start the network name resource.  
  
        3.  Use [Add-ClusterResourceDependency](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461014(v=technet.10)) to set the dependency between the network name and the existing SQL Server Availability Group resource.  
  
         For information about using Windows PowerShell for failover clusters, see [Overview of Server Manager Commands](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732757(v=ws.11)#BKMK_wps).  
  
2.  Start [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] listening on the new listener. After creating the additional listener, connect to the instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] that hosts the primary replica of the availability group and use [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)], or PowerShell to modify the listener port.  
  
 For more information, see [How to create multiple listeners for same availability group](/archive/blogs/sqlalwayson/how-to-create-multiple-listeners-for-same-availability-group-goden-yao) (a SQL Server Always On team blog).  
  
 
  
## Next steps

Now that you've created your listener, configure your application to [connect to the listener](listeners-client-connectivity-application-failover.md). You can also review various [availability group monitoring strategies](monitoring-of-availability-groups-sql-server.md) to ensure the health of your availability group.

You can also [view the properties of a listener](view-availability-group-listener-properties-sql-server.md) or learn how to [remove the listener](remove-an-availability-group-listener-sql-server.md), if necessary.
