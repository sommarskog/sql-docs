---
title: "Microsoft Connector for SAP BW"
description: "Microsoft Connector for SAP BW"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# Microsoft Connector for SAP BW

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  The [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW consists of a set of three components that let you extract data from, or load data into, an SAP Netweaver BW version 7 system.  
  
 The [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW for SQL Server 2016 is a component of the SQL Server 2016 Feature Pack. To install the Connector for SAP BW and its documentation, download and run the installer from the [SQL Server 2016 Feature Pack web page](https://www.microsoft.com/download/details.aspx?id=56833).  

> [!IMPORTANT]
> Microsoft does not anticipate providing an updated version of the Connector for SAP BW. Microsoft does not own the source code for the SAP BW components, which were developed by a third party, and as a result cannot update them. Consider purchasing the latest SAP connectivity components from a Microsoft ISV partner such as [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html). Microsoft's ISV partners have adapted their SAP connectivity components for SSIS for installation in Azure.
 
> [!IMPORTANT]  
>  The documentation for the Microsoft Connector for SAP BW assumes familiarity with the SAP Netweaver BW environment. For more information about SAP Netweaver BW, or for information about how to configure SAP Netweaver BW objects and processes, see your SAP documentation.  
  
> [!IMPORTANT]  
>  Extracting data from SAP Netweaver BW requires additional SAP licensing. Check with SAP to verify these requirements.  
  
## Components  
 The [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW has the following components:  
  
-   **SAP BW Source**-The SAP BW source is a data flow source component that lets you extract data from an SAP Netweaver BW version 7 system.  
  
-   **SAP BW Destination**-The SAP BW destination is a data flow destination component that lets you load data into an SAP Netweaver BW version 7 system.  
  
-   **SAP BW Connection Manager**-The SAP BW connection manager connects either an SAP BW source or SAP BW destination to an SAP Netweaver BW version 7 system.  
  
 For a walkthrough that demonstrates how to configure and use the SAP BW connection manager, source, and destination, see the white paper, [Using SQL Server Integration Services with SAP BI 7.0](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100)). This white paper also shows how to configure the required objects in SAP BW.  
  
## Documentation  
 This Help file for the [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW contains the following topics and sections:  
  
 [Installing the Microsoft Connector for SAP BW](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 Describes the installation requirements for the [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Microsoft Connector for SAP BW Components](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 Describes each component of the [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Microsoft Connector for SAP BW F1 Help](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 Describes the user interface of each component of the [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
