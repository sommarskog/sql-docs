---
title: "Using Strong-Named Custom Assemblies"
description: Learn to use a strong-named custom assembly to uniquely identify an assembly to the common language runtime (CLR) and ensure binary integrity.
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: custom-assemblies
ms.topic: reference
ms.custom: updatefrequency5
helpviewer_keywords:
  - "AllowPartiallyTrustedCallersAttribute attribute"
  - "strong-named custom assemblies [Reporting Services]"
  - "strong names [Reporting Services]"
  - "assemblies [Reporting Services], strong names"
  - "custom assemblies [Reporting Services], strong-named"
---
# Using Strong-Named Custom Assemblies
  A strong name identifies an assembly and includes the assembly's text name, four-part version number, culture information (if provided), a public key, and a digital signature stored in the assembly's manifest. A strong name uniquely identifies an assembly to the common language runtime (CLR) and ensures binary integrity.  
  
## Using AllowPartiallyTrustedCallersAttribute  
 To use strong-named assemblies with reports, you must allow your strong-named assembly to be called by partially trusted code using the assembly's **AllowPartiallyTrustedCallers** attribute. You can use **AllowPartiallyTrustedCallersAttribute** to allow strong-named assemblies to be called by Report Designer or the report server in report expressions. To allow partially trusted code to call strong-named assemblies, add the following assembly-level attribute to your assembly attribute file.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** is effective only when applied by a strong-named assembly at the assembly level. For more information about applying attributes at the assembly level, see "Applying Attributes" in the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK documentation.  
  
> [!CAUTION]  
>  When **AllowPartiallyTrustedCallersAttribute** is present, the default **FullTrustLinkDemand** security checks are prevented, making the assembly callable from any other partially trusted assembly. All security checks, including class-level or method-level declarative security attributes, must be explicitly stated.  
  
## See Also  
 [Using Custom Assemblies with Reports](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
