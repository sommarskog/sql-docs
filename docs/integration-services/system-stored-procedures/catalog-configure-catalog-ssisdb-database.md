---
title: "catalog.configure_catalog (SSISDB Database)"
description: "catalog.configure_catalog (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.configure_catalog (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Configures the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog by setting a catalog property to a specified value.  
  
## Syntax  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## Arguments  
 [ @property_name = ] *property_name*  
 The name of the catalog property. The *property_name* is **nvarchar(255)**. For more information about available properties, see [catalog.catalog_properties &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value = ] *property_value*  
 The value of the catalog property. The *property_value* is **nvarchar(255)**. For more information about property values, see [catalog.catalog_properties &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
 None  
  
## Remarks  
 This stored procedure determines whether the *property_value* is valid for each *property_name*.  
  
 This stored procedure can be performed only when there are no active executions, such as pending, queued, running, and paused executions.  
  
 While the catalog is being configured, all other catalog stored procedures fail with the error message "Server is currently being configured."
  
 When the catalog is configured, an entry is written to the operation log.  
  
## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes some conditions that may raise an error or warning:  
  
-   The property does not exist  
  
-   The property value is invalid  
  
  
