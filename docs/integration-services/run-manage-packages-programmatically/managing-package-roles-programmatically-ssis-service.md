---
title: "Managing Package Roles Programmatically (SSIS Service)"
description: "Managing Package Roles Programmatically (SSIS Service)"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "reference"
helpviewer_keywords:
  - "Integration Services packages, roles"
  - "roles [Integration Services]"
  - "packages [Integration Services], roles"
---
# Managing Package Roles Programmatically (SSIS Service)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  As you work programmatically with [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] packages, you may want to determine which roles are available to apply to packages, or to determine or set the roles applied to an individual package. The <xref:Microsoft.SqlServer.Dts.Runtime.Application> class of the <xref:Microsoft.SqlServer.Dts.Runtime> namespace provides a variety of methods to satisfy these requirements.  
  
 Roles apply only to packages stored in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** database. For more information about package roles, see [Integration Services Roles &#40;SSIS Service&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 All the methods discussed in this topic require a reference to the **Microsoft.SqlServer.ManagedDTS** assembly. After you add the reference in a new project, import the <xref:Microsoft.SqlServer.Dts.Runtime> namespace by using a **using** or **Imports** statement.  
  
> [!IMPORTANT]  
>  The methods of the <xref:Microsoft.SqlServer.Dts.Runtime.Application> class for working with the SSIS Package Store support only ".", localhost, or the server name for the local server. You cannot use "(local)".  
  
## Determining Which Roles Are Available  
 To determine which roles are available for the packages stored on a particular server, call the <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> method of the <xref:Microsoft.SqlServer.Dts.Runtime.Application> class.  
  
## Determining Which Roles Are Assigned  
 To determine which roles have already been assigned to a particular package, call the <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> method. To assign roles to a package, call the <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> method.  
  
## See Also  
 [Integration Services Roles &#40;SSIS Service&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
