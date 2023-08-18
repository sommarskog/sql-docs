---
title: "Roles and Permissions (Reporting Services)"
description: "Roles and Permissions (Reporting Services)"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/01/2017
ms.service: reporting-services
ms.subservice: security
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "access controls [Reporting Services]"
  - "permissions [Reporting Services], about permissions"
  - "security [Reporting Services], identity and access control"
  - "authentication [Reporting Services]"
  - "permissions [Reporting Services]"
  - "security [Reporting Services], role-based"
  - "identity [Reporting Services]"
---
# Roles and Permissions (Reporting Services)
  Reporting Services provides an authentication subsystem and role-based authorization model. Authentication and authorization models vary depending on whether the report server runs in native mode or SharePoint mode. If the report server is part of a SharePoint deployment, SharePoint permissions determine who has access to the report server.  
  
## Identity and Access Control for Native Mode  
 Default authentication is based on Windows Authentication and integrated security. You can change the authentication settings to allow the report server to respond to different authentication requests, or even replace the default security features with a custom authentication extension that you provide.  
  
 Authorization is based on roles that you assign to a principal. Each role consists of a set of related tasks, which are in turn composed of related operations. For example, the **Manage reports** task grants access to the following report server operations: view reports, add report, update report, delete report, schedule report, and update report properties.  
  
## Identity and Access Control for SharePoint Mode  
 In SharePoint integrated mode, authentication and authorization are handled on the SharePoint site, before requests reach the report server. Depending on how you configure authentication, requests from a SharePoint site include a security token or a trusted user name. Permissions that you set for SharePoint users and groups authorize access to report server items that are placed in SharePoint libraries.  
  
## In This Section  
 [Granting Permissions on a Native Mode Report Server](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 Describes the role-based authorization model that provides access to content and operations.  
  
 [Granting Permissions on Report Server Items on a SharePoint Site](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 Explains how SharePoint groups, permission levels, and permissions are used to control access to a report server.  
  
## See Also  
 [Authentication with the Report Server](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Granting Permissions on a Native Mode Report Server](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
