---
title: "Configure cluster quorum NodeWeight settings"
description: Describes how to configure the NodeWeight settings for a member node in a Windows Server Failover Cluster.
author: MashaMSFT
ms.author: mathoma
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: failover-cluster-instance
ms.topic: how-to
helpviewer_keywords:
  - "Availability Groups [SQL Server], WSFC clusters"
  - "quorum [SQL Server], AlwaysOn and WSFC quorum"
  - "quorum [SQL Server], Always On and WSFC quorum"
---
# Configure Cluster Quorum NodeWeight Settings
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to configure NodeWeight settings for a member node in a Windows Server Failover Clustering (WSFC) cluster. NodeWeight settings are used during quorum voting to support disaster recovery and multi-subnet scenarios for [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] and [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Failover Cluster Instances.  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **To view quorum NodeWeight settings using:** [Using Powershell](#PowerShellProcedure), [Using Cluster.exe](#CommandPromptProcedure)  
  
-   [Related Content](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Before You Start  
  
###  <a name="Prerequisites"></a> Prerequisites  
 This feature is supported only in [!INCLUDE[winserver2008](../../../includes/winserver2008-md.md)] or later versions.  
  
> [!IMPORTANT]  
>  In order to use NodeWeight settings, the following hotfix must be applied to all servers in the WSFC cluster:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): A hotfix is available to let you configure a cluster node that does not have quorum votes in [!INCLUDE[winserver2008](../../../includes/winserver2008-md.md)] and in [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  If this hotfix is not installed, the examples in this topic will return empty or NULL values for NodeWeight.  
  
###  <a name="Security"></a> Security  
 The user must be a domain account that is member of the local Administrators group on each node of the WSFC cluster.  
  
##  <a name="PowerShellProcedure"></a> Using Powershell  
  
##### To configure NodeWeight settings  
  
1.  Start an elevated Windows PowerShell via **Run as Administrator**.  
  
2.  Import the `FailoverClusters` module to enable cluster commandlets.  
  
3.  Use the `Get-ClusterNode` object to set the `NodeWeight` property for each node in the cluster.  
  
4.  Output the cluster node properties in a readable format.  
  
### Example (Powershell)  
 The following example changes the NodeWeight setting to remove the quorum vote for the "AlwaysOnSrv1" node, and then outputs the settings for all nodes in the cluster.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "AlwaysOnSrv1"  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Using Cluster.exe  
  
> [!NOTE]  
>  The cluster.exe utility is deprecated in the [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] release.  Please use PowerShell with Failover Clustering for future development.  The cluster.exe utility will be removed in the next release of Windows Server. For more information, see [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### To configure NodeWeight settings  
  
1.  Start an elevated Command Prompt via **Run as Administrator**.  
  
2.  Use **cluster.exe** to set `NodeWeight` values.  
  
### Example (Cluster.exe)  
 The following example changes the NodeWeight value to remove the quorum vote of the "AlwaysOnSrv1" node in the "Cluster001" cluster.  
  
```ms-dos  
cluster.exe Cluster001 node AlwaysOnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> Related Content  
  
-   [View Events and Logs for a Failover Cluster](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog Failover Cluster Cmdlet](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461045(v=technet.10))  
  
## See Also  
 [WSFC Quorum Modes and Voting Configuration &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [View Cluster Quorum NodeWeight Settings](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [Failover Cluster Cmdlets in Windows PowerShell Listed by Task Focus](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
