---
title: SQL Server Data Tools
description: View resources on database development tasks that you can accomplish with SQL Server Data Tools, such as designing tables and creating feature extensions.
author: markingmyname
ms.author: maghan
ms.date: 08/11/2023
ms.service: sql
ms.subservice: ssdt
ms.topic: conceptual
f1_keywords:
  - "sql.data.tools.errortask.generichelp"
  - "sql.data.tools.sqlserverobjectexplorer"
---

# SQL Server Data Tools

**SQL Server Data Tools (SSDT)** is a modern development tool for building SQL Server relational databases, databases in Azure SQL, Analysis Services (AS) data models, Integration Services (IS) packages, and Reporting Services (RS) reports. With SSDT, you can design and deploy any SQL Server content type with the same ease as you would develop an application in Visual Studio.

The core of SQL Server Data Tools functionality is available as a workload component with Visual Studio, which enables developing databases.  Additional functionality for developing AS, IS, and RS projects is available as Visual Studio extensions for installation in addition to the SSDT workload. The Visual Studio extensions are available from the Visual Studio Marketplace and more information on installing SSDT can be found in [Download SQL Server Data Tools](download-sql-server-data-tools-ssdt.md).

## Release notes

The latest release notes for SQL Server Data Tools with Visual Studio 2022 can be found in the following locations:

- SQL Server Data Tools (SSDT) release notes are listed with the [release notes for Visual Studio 2022](/visualstudio/releases/2022/release-notes)
- Analysis Services (SSAS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects2022)
- Integration Services (SSIS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=SSIS.MicrosoftDataToolsIntegrationServices)
- Reporting Services (SSRS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio2022)

The release notes for SQL Server Data Tools with Visual Studio 2019 can be found in the following locations:
- SQL Server Data Tools (SSDT) release notes are listed with the [release notes for Visual Studio 2019](/visualstudio/releases/2019/release-notes)
- Analysis Services (SSAS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
- Integration Services (SSIS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=SSIS.SqlServerIntegrationServicesProjects)
- Reporting Services (SSRS) extension release notes are listed on the [extension marketplace](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)

For information about SQL Server Data Tools with Visual Studio 2017, see [Previous releases of SQL Server Data Tools (SSDT and SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).

## Core SQL Server Data Tools

SQL Server Data Tools (SSDT) transforms database development by introducing a ubiquitous, declarative model (SQL database projects) that spans all the phases of database development inside Visual Studio. You can use SSDT Transact\-SQL design capabilities to build, debug, maintain, and refactor databases. You can work with a database project or directly connect to a database instance on or off-premise.  
  
Developers can use familiar Visual Studio tools for database development. Tools such as: code navigation, IntelliSense, language support that parallels what is available for C# and Visual Basic, platform-specific validation, debugging, and declarative editing in the Transact\-SQL editor. SSDT also provides a visual Table Designer for creating and editing tables in either database projects or connected database instances. While you are working on your database projects in a team-based environment, you can use version control for all the files. When it's time to publish your project, you can publish to all supported SQL platforms; including SQL Database and SQL Server. SSDT platform validation capability ensures that your scripts work on the target you specify.  
  
The SQL Server Object Explorer in Visual Studio offers a view of your database objects similar to SQL Server Management Studio. SQL Server Object Explorer allows you to do light-duty database administration and design work. You can easily create, edit, rename and delete tables, stored procedures, types, and functions. You can also edit table data, compare schemas, or execute queries by using contextual menus right from the SQL Server Object Explorer.  
  
The following topics and sections discuss how SSDT can help you do database development. How To topics are included to help guide you through completing tasks for your database project. These tasks, written like a tutorial and completed in order, use Northwind Traders, a fictitious company that imports and exports specialty foods.  
  
|Topics/Section|Description|  
|-------------------|---------------|  
|[Project-Oriented Offline Database Development](../ssdt/project-oriented-offline-database-development.md)|Topics in this section describe SQL Server Data Tools features for authoring, building, debugging and publishing a database project.|  
|[Project-Oriented Database Development using Command-Line Tools](../ssdt/project-oriented-database-development-using-command-line-tools.md)|Topics in this section describe command-line tools which enable a number of project-oriented database development scenarios.|  
|[Connected Database Development](../ssdt/connected-database-development.md)|Topics in this section describe SQL Server Data Tools features for designing and querying a connected database.|  
|[Compare and Synchronize Data in One or More Tables with Data in a Reference Database](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)|Discusses how to compare data in a source database and a target database, specify which values should match, and then either update the target to synchronize the databases or export the update script to the Transact\-SQL editor or to a file.|  
|[Use Transact-SQL Editor to Edit and Execute Scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)|Topics in this section describe how to use the Transact\-SQL Editor, which provides a rich editing and debugging experience when working with scripts.|  
|[Manage Tables, Relationships, and Fix Errors](../ssdt/manage-tables-relationships-and-fix-errors.md)|Topics in this section describe how to:<br /><br />-   Use the Table Designer to design tables and manage table relationships.<br />-   Fix common syntax or semantic errors.|  
|[Verifying Database Code by Using SQL Server Unit Tests](../ssdt/verifying-database-code-by-using-sql-server-unit-tests.md)|Discusses how you can use SQL Server unit tests to establish a baseline state for your database and then to verify any subsequent changes that you make to database objects.|  
|[Extending the Database Features](../ssdt/extending-the-database-features.md)|You can create feature extensions that let you extend features such as unit testing, and database code analysis.|  
|[Required Permissions for SQL Server Data Tools](../ssdt/required-permissions-for-sql-server-data-tools.md)|Discusses required access permission to use SQL Server Data Tools.|  
|[DAC Framework Compatibility](../ssdt/dac-framework-compatibility.md)|Describes compatibility issues with DAC framework.|  
  

  
