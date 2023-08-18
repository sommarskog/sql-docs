---
title: "namespace-uri-from-QName (XQuery)"
description: Learn how to use the namespace-uri-from-QName function to retrieve the namespace URI of a QName.
author: "rothja"
ms.author: "jroth"
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "language-reference"
helpviewer_keywords:
  - "fn:namespace-uri-from-QName function"
  - "namespace-uri-from-QName function"
dev_langs:
  - "XML"
---
# Functions Related to QNames - namespace-uri-from-QName
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sqlserver.md)]

  Returns a string representing the namespace uri of the QName specified by *$arg*. The result is the empty sequence if *$arg* is the empty sequence.  
  
## Syntax  
  
```  
namespace-uri-from-QName($arg as xs:QName?) as xs:string?  
```  
  
## Arguments  
 *$arg*  
 Is the QName whose namespace URI is returned.  
  
## Examples  
 This topic provides XQuery examples against XML instances that are stored in various **xml** type columns in the AdventureWorks database.  
  
### A. Retrieve the namespace URI from a QName  
 For a working sample, see [local-name-from-QName &#40;XQuery&#41;](../xquery/functions-related-to-qnames-local-name-from-qname.md).  
  
### Implementation Limitations  
 These are the limitations:  
  
-   The **namespace-uri-from-QName()** function returns instances of xs:string instead of xs:anyURI.  
  
## See Also  
 [Functions Related to QNames &#40;XQuery&#41;](./functions-related-to-qnames-expanded-qname.md)  
  
