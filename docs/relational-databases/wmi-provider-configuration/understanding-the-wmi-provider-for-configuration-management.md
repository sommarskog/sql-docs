---
title: "WMI Provider for Configuration Management"
description: Learn how the WMI Provider for Configuration Management uses WMI to manage services, server aliases, and client/server network settings in SQL Server.
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: wmi
ms.topic: "reference"
helpviewer_keywords:
  - "WMI Provider for Configuration Management, operations supported"
---
# Understanding the WMI Provider for Configuration Management
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provides the WMI Provider for Configuration Management. This lets you use Windows Management Instrumentation (WMI) to manage [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client and server network settings, and server aliases. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services, network settings, and aliases are represented by WMI objects in the root\Microsoft\SqlServer\ComputerManagement*nn* namespace of the computer. After a connection is established with the WMI provider on the specified computer, the services, network settings, and aliases can be queried using WQL or a scripting language.  
  
 The WMI Provider is an instance provider. It supplies instances of the [WMI Classes](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) and supports the following asynchronous operations.  
  
 Instance retrieval  
 Retrieval of a particular class type instance.  
  
 Enumeration  
 Enumeration of all instances of a class type.  
  
 Modification  
 Modification of a particular instance of a class type.  
  
 Classes have methods that allow the modification of their properties.  
  
 Deletion  
 Removing a particular instance of a class type.  
  
 Query processing  
 Enumeration of instances of a class type based on a filter.  
  
 For examples of management application using the WMI Provider for Configuration Management, see [Using WQL and Scripting Languages with the WMI Provider for Configuration Management](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 For more information about programming management applications using the WMI Provider, see the WMI documentation in the [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK.  
  
## See Also  
 [Working with the WMI Provider for Configuration Management](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Using WQL and Scripting Languages with the WMI Provider for Configuration Management](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
