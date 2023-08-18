---
title: "Availability group wizard: Specify availability group options"
description: "Describes the options found on the 'Specify Availability Group Name' page of the Availability Group Wizard within SQL Server Management Studio."
author: MashaMSFT
ms.author: mathoma
ms.date: "05/17/2016"
ms.service: sql
ms.subservice: availability-groups
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.newagwizard.specifyagname.f1"
  - "sql13.swb.adddatabasewizard.specifyagname.f1"
---
# Specify Availability Group Options Page for an Always On Availability Group
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  This topic describes the options of the **Specify Availability Group Name** page. This topic is used by both the [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] and [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] of [!INCLUDE[ssnoversion](../../../includes/ssnoversion-md.md)].  
  
##  <a name="PageOptions"></a> Specify Availability Group Options  
 **Availability group name**  
 Specify the name of the availability group. For a new availability group, specify a valid [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identifier that is unique across all availability groups in the Windows Server failover cluster (WSFC). The maximum length for an availability group name is 128 characters.  

 **Cluster type** 
 Next, specify the cluster type. The possible cluster types depend on the [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] version and operating system. Choose one from the following list:

   * **Windows Server Failover Clustering**
   
      Use when the availability group is hosted on instances of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] that belong to a Windows Server failover cluster for high availability and disaster recovery. Applies to all supported versions of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 

   * **EXTERNAL**
      
      Use when the availability group is hosted on an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] that is managed by an external cluster technology for high availability and disaster recovery, for example Pacemaker on Linux. Applies to [!INCLUDE[sssql14](../../../includes/sssql17-md.md)] and later.
      
>[!IMPORTANT]
> Do not choose **cluster type** = `EXTERNAL` on a Windows platform. Doing so will result in the availability group going into a resolving state and will prevent you from removing databases from the availability group. 

   * **NONE**
      
      Use when the availability group is hosted on an instance of [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] that is not managed by a cluster technology for read scale and load balancing. Applies to [!INCLUDE[sssql14](../../../includes/sssql17-md.md)] and later. 
 
   **Database level health detection**
   Check this box to enable database level health detection (DB_FAILOVER) option for the availability group. The database health detection notices when a database is no longer in the online status, when something goes wrong and will trigger the automatic failover of the availability group. See 
   [SQL Server Always On Database Health Detection Failover Option](sql-server-always-on-database-health-detection-failover-option.md).


Select Databases Page (New Availability Group Wizard and Add Database Wizard)  
  
##  <a name="LaunchWiz"></a> Related Tasks  
  
-   [Use the New Availability Group Dialog Box &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Use the Add Database to Availability Group Wizard &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## See Also  
 [Overview of Always On Availability Groups &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
