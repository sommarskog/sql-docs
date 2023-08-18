---
title: Use T-SQL (CREATE EXTERNAL LIBRARY) to install R packages
description: Add new R packages to SQL Server 2016 R Services or SQL Server Machine Learning Services (In-Database).
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: 11/20/2019
ms.service: sql
ms.subservice: machine-learning-services
ms.topic: how-to
ms.custom: intro-installation
monikerRange: "=sql-server-2017"
---

# Use T-SQL (CREATE EXTERNAL LIBRARY) to install R packages on SQL Server
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

This article explains how to install new R packages on an instance of SQL Server where machine learning is enabled. There are multiple approaches to choose from. Using T-SQL works best for server administrators who are unfamiliar with R.

The [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) statement makes it possible to add a package or set of packages to an instance or a specific database without running R or Python code directly. However, this method requires package preparation and additional database permissions.

+ All packages must be available as a local zipped file, rather than downloaded on demand from the internet.

+ All dependencies must be identified by name and version, and included in the zip file. The statement fails if required packages are not available, including downstream package dependencies. 

+ You must be **db_owner** or have CREATE EXTERNAL LIBRARY permission in a database role. For details, see [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## Download packages in archive format

If you are installing a single package, download the package in zipped format.

It's more common to install multiple packages due to package dependencies. When a package requires other packages, you must verify that all of them are accessible to each other during installation. We recommend [creating a local repository](create-a-local-package-repository-using-minicran.md) using [miniCRAN](https://andrie.github.io/miniCRAN/) to assemble a full collection of packages, as well as [igraph](https://igraph.org/r/) for analyzing packages dependencies. Installing the wrong version of a package or omitting a package dependency can cause a CREATE EXTERNAL LIBRARY statement to fail. 

## Copy the file to a local folder

Copy the zipped file containing all packages to a local folder on the server. If you do not have access to the file system on the server, you can also pass a complete package as a variable, using a binary format. For more information, see [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## Run the statement to upload packages

Open a **Query** window, using an account with administrative privileges.

Run the T-SQL statement `CREATE EXTERNAL LIBRARY` to upload the zipped package collection to the database.

For example, the following statement names as the package source a miniCRAN repository containing the **randomForest** package, together with its dependencies. 

```sql
CREATE EXTERNAL LIBRARY [randomForest]
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

You cannot use an arbitrary name; the external library name must have the same name that you expect to use when loading or calling the package.

## Verify package installation

If the library is successfully created, you can run the package in SQL Server, by calling it inside a stored procedure.
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## See also

+ [Get R package information](r-package-information.md)
+ [R tutorials](../tutorials/r-tutorials.md)
