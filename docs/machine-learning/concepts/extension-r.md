---
title: R language extension
description: Learn about the R extension for running external R scripts with SQL Server Machine Learning Services and SQL Server R Services.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: 05/24/2022
ms.service: sql
ms.subservice: machine-learning-services
ms.topic: conceptual
monikerRange: ">=sql-server-2016||>=sql-server-linux-ver15"
---
# R language extension in SQL Server Machine Learning Services
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

This article describes the R extension for running external Python scripts with [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) and [SQL Server 2016 R Services](../r/sql-server-r-services.md). The extension adds:

- An R execution environment
- Base R distribution with standard libraries and tools
- Microsoft R libraries:
  - [RevoScaleR](../r/ref-r-revoscaler.md) for analytics at scale
  - [MicrosoftML](../r/ref-r-microsoftml.md) for machine learning algorithms. **Applies only to SQL Server 2016, SQL Server 2017, and SQL Server 2019.**
  - Other libraries for accessing data or R code in SQL Server

## R components

SQL Server includes both open-source and proprietary packages. The base R libraries are installed through Microsoft's distribution of open-source R: Microsoft R Open (MRO). Current users of R should be able to port their R code and execute it as an external process on SQL Server with few or no modifications. MRO is installed independently of SQL tools, and is executed outside of core engine processes, in the extensibility framework. During installation, you must consent to the terms of the open-source license. Thereafter, you can run standard R packages without further modification just as you would in any other open-source distribution of R. 

::: moniker range="=sql-server-2016||=sql-server-2017||=sql-server-ver15"
For [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)], [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], and [!INCLUDE[sssql19-md](../../includes/sssql19-md.md)], SQL Server does not modify the base R executables, but you must use the version of R installed by Setup because that version is the one that the proprietary packages are built and tested on. For more information about how MRO differs from a base distribution of R that you might get from CRAN, see [Interoperability with R language and Microsoft R products and features](/r-server/what-is-r-server-interoperability).

The R base package distribution installed by Setup can be found in the folder associated with the instance. For example, if you installed R Services on a SQL Server default instance, the R libraries are located in this folder by default: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. Similarly, the R tools associated with the default instance would be located in this folder by default: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

R packages added by Microsoft for parallel and distributed workloads include the following libraries.

| Library | Description |
|---------|-------------|
| [**RevoScaleR**](/machine-learning-server/r-reference/revoscaler/revoscaler) | Supports data source objects and data exploration, manipulation, transformation, and visualization. It supports creation of remote compute contexts, as well as a various scalable machine learning models, such as **rxLinMod**. The APIs have been optimized to analyze data sets that are too big to fit in memory and to perform computations distributed over several cores or processors. The RevoScaleR package also supports the XDF file format for faster movement and storage of data used for analysis. The XDF format uses columnar storage, is portable, and can be used to load and then manipulate data from various sources, including text, SPSS, or an ODBC connection. |
| [**MicrosoftML**](/r-server/r/concept-what-is-the-microsoftml-package) | Contains machine learning algorithms that have been optimized for speed and accuracy, as well as in-line transformations for working with text and images. For more information, see [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md). **Applies only to SQL Server 2016, SQL Server 2017, and SQL Server 2019.**| 
::: moniker-end

::: moniker range=">=sql-server-ver16"
Beginning with [!INCLUDE [sssql22-md](../../includes/sssql22-md.md)], runtimes for R, Python, and Java, are no longer installed with SQL Setup. Instead, install your desired R and/or Python custom runtime(s) and packages. For more information, see [Install SQL Server 2022 Machine Learning Services on Windows](../install/sql-machine-learning-services-windows-install-sql-2022.md) or [Install SQL Server Machine Learning Services (Python and R) on Linux](../../linux/sql-server-linux-setup-machine-learning.md).
::: moniker-end

## Using R in SQL Server

You can script R using base functions, but to benefit from multi-processing, you must import the **RevoScaleR** and **MicrosoftML** modules into your R code, and then call its functions to create models that execute in parallel. 
 
Supported data sources include ODBC databases, SQL Server, and XDF file format to exchange data with other sources, or with R solutions. Input data must be tabular. All R results must be returned in the form of a data frame.

Supported compute contexts include local, or remote SQL Server compute context. A remote compute context refers to code execution that starts on one computer such as a workstation, but then switches script execution to a remote computer. Switching the compute context requires that both systems have the same RevoScaleR library.

Local compute context, as you might expect, includes execution of R code on the same server as the database engine instance, with code inside T-SQL or embedded in a stored procedure. You can also run the code from a local R IDE and have the script execute on the SQL Server computer, by defining a remote compute context.

## Execution architecture

The following diagrams depict the interaction of SQL Server components with the R runtime in each of the supported scenarios: running script in-database, and remote execution from an R command line, using a SQL Server compute context.

### R scripts executed from SQL Server in-database

R code that is run from "inside" SQL Server is executed by calling a stored procedure. Thus, any application that can make a stored procedure call can initiate execution of R code.  Thereafter SQL Server manages the execution of R code as summarized in the following diagram.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. A request for the R runtime is indicated by the parameter _@language='R'_ passed to the stored procedure, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). SQL Server sends this request to the launchpad service.
In Linux, SQL uses a **launchpadd** service to communicate with a separate launchpad process for each user. See the [Extensibility architecture diagram](extensibility-framework.md#architecture-diagram) for details.
2. The launchpad service starts the appropriate launcher; in this case, RLauncher.
3. RLauncher starts the external R process.
4. BxlServer coordinates with the R runtime to manage exchanges of data with SQL Server and storage of working results.
5. SQL Satellite manages communications about related tasks and processes with SQL Server.
6. BxlServer uses SQL Satellite to communicate status and results to SQL Server.
7. SQL Server gets results and closes related tasks and processes.

### R scripts executed from a remote client

When connecting from a remote data science client that supports Microsoft R, you can run R functions in the context of SQL Server by using the RevoScaleR functions. This is a different workflow from the previous one, and is summarized in the following diagram.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. For RevoScaleR functions, the R runtime calls a linking function which in turn calls BxlServer.
2. BxlServer is provided with Microsoft R and runs in a separate process from the R runtime.
3. BxlServer determines the connection target and initiates a connection using ODBC, passing credentials supplied as part of the connection string in the R data source object.
4. BxlServer opens a connection to the SQL Server instance.
5. For an R call, the launchpad service is invoked, which is turn starts the appropriate launcher, RLauncher. Thereafter, processing of R code is similar to the process for running R code from T-SQL.
6. RLauncher makes a call to the instance of the R runtime that is installed on the SQL Server computer.
7. Results are returned to BxlServer.
8. SQL Satellite manages communication with SQL Server and cleanup of related job objects.
9. SQL Server passes results back to the client.

## See also

+ [Extensibility framework in SQL Server](extensibility-framework.md)
+ [Python and machine learning extensions in SQL Server](extension-python.md)
