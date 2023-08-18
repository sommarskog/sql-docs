---
title: "Integration Services Programming Overview"
description: "Integration Services Programming Overview"
author: chugugrace
ms.author: chugu
ms.reviewer: maghan
ms.date: 07/13/2023
ms.service: sql
ms.subservice: integration-services
ms.topic: "reference"
helpviewer_keywords:
  - "Integration Services, programming"
  - "architecture [Integration Services]"
  - "assemblies [Integration Services]"
  - "SSIS, programming"
  - "SQL Server Integration Services, programming"
  - "run-time engine [Integration Services]"
  - "packages [Integration Services], programming"
  - "data flow engine [Integration Services]"
  - "languages [Integration Services]"
---

# Integration Services Programming Overview

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] has an architecture that separates data movement and transformation from package control flow and management. There are two distinct engines that define this architecture and that can be automated and extended when programming [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. The run-time engine implements the control flow and package management infrastructure that lets developers control the flow of execution and set options for logging, event handlers, and variables. The data flow engine is a specialized, high performance engine that is exclusively dedicated to extracting, transforming, and loading data. When programming [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], you'll be programming against these two engines.

The following image depicts the architecture of [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

:::image type="content" source="../integration-services/media/mw-dts-01.gif" alt-text="Integration Services architecture.":::

## Integration Services Run-time Engine

The [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] run-time engine controls the management and execution of packages, by implementing the infrastructure that enables execution order, logging, variables, and event handling. Programming the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] run-time engine lets developers automate the creation, configuration, and execution of packages and create custom tasks and other extensions.

For more information, see [Extending the Package with the Script Task](../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md), [Developing a Custom Task](../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md), and [Building Packages Programmatically](../integration-services/building-packages-programmatically/building-packages-programmatically.md).

## Integration Services Data Flow Engine

The data flow engine manages the data flow task, which is a specialized, high performance task dedicated to moving and transforming data from disparate sources. Unlike other tasks, the data flow task contains additional objects called data flow components, which can be sources, transformations, or destinations. These components are the core moving parts of the task. They define the movement and transformation of data. Programming the data flow engine lets developers automate the creation and configuration of the components in a data flow task, and create custom components.

For more information, see [Extending the Data Flow with the Script Component](../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md), [Developing a Custom Data Flow Component](../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md), and [Building Packages Programmatically](../integration-services/building-packages-programmatically/building-packages-programmatically.md).

## Supported Languages

[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fully supports the [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. This lets developers program [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in their choice of .NET-compliant languages. Although both the run-time engine and the data flow engine are written in native code, they're both available through a fully managed object model.

You can program [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] packages, custom tasks, and components in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] or in another code or text editor. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] offers the developer many tools and features to simplify and accelerate the iterative cycles of coding, debugging, and testing. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] also makes deployment easier. However, you don't need [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] to compile and build [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] code projects. The [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK includes the [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] and [!INCLUDE[csprcs](../includes/csprcs-md.md)] compilers and related tools.

> [!IMPORTANT]  
> By default, the [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] is installed with [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], but the [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK is not. Unless the SDK is installed on the computer and the SDK documentation is included in the Books Online collection, links to SDK content in this section will not work. After you have installed the [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK, you can add the SDK documentation to the Books Online collection and table of contents by following the instructions in [Add or Remove Product Documentation for SQL Server](https://www.microsoft.com/download/details.aspx?id=42557).

The [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Script task and Script component use [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) as an embedded scripting environment. VSTA supports [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic and [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#.

> [!NOTE]  
> The [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] application programming interfaces are incompatible with COM-based scripting languages such as VBScript.

## Locate Assemblies

In [!INCLUDE[ssSQL19](../includes/sssql19-md.md)], the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] assemblies were upgraded to .NET 4.0. There's a separate global assembly cache for .NET 4, located in `*\<drive>*:\Windows\Microsoft.NET\assembly`. You can find all of the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] assemblies under this path, usually in the GAC_MSIL folder.

As in previous versions of [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], the core [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] extensibility .dll files are also located at `*\<drive>*:\Program Files\Microsoft SQL Server\\\<nnn>\SDK\Assemblies`. `<nnn>` identifies the version of [SQL Server shared Files location](../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md#shared-files-for-all-instances-of-).

## Commonly Used Assemblies

The following table lists the assemblies that are frequently used when programming [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] using the [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].

| Assembly | Description |
| --- | --- |
| Microsoft.SqlServer.ManagedDTS.dll | Contains the managed run-time engine. |
| Microsoft.SqlServer.RuntimeWrapper.dll | Contains the primary interop assembly (PIA), or wrapper, for the native run-time engine. |
| Microsoft.SqlServer.PipelineHost.dll | Contains the managed data flow engine. |
| Microsoft.SqlServer.PipelineWrapper.dll | Contains the primary interop assembly (PIA), or wrapper, for the native data flow engine. |
