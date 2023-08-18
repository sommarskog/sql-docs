---
title: WITH XMLNAMESPACES (Transact-SQL)
description: "WITH XMLNAMESPACES"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "WITH_XMLNAMESPACES_TSQL"
  - "WITH XMLNAMESPACES"
helpviewer_keywords:
  - "adding XML namespaces"
  - "XML namespace declarations [SQL Server]"
  - "clauses [SQL Server], WITH XMLNAMESPACES"
  - "WITH XMLNAMESPACES clause"
  - "declaring XML namespaces"
dev_langs:
  - "TSQL"
---
# WITH XMLNAMESPACES
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Declares one or more XML namespaces.  
  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```syntaxsql
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```syntaxsql
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *xml_namespace_uri*  
 A Uniform Resource Identifier (URI) that identifies the XML namespace that is being declared. *xml_namespace_uri* is an SQL string.  
  
 *xml_namespace_prefix*  
 Specifies a prefix to be mapped and associated with the namespace URI value specified in *xml_namespace_uri*. *xml_namespace_prefix* must be a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifier.  
  
## Remarks  
 When you use the WITH XMLNAMESPACES clause in a statement that also includes a common table expression, the WITH XMLNAMESPACES clause must precede the common table expression in the statement.  
  
 The following are general syntax rules that apply when you use the WITH XMLNAMESPACES clause:  
  
-   Each XML namespace declaration must contain at least one XML default namespace declaration item.  
  
-   Each XML namespace prefix used must be a non-colonized name (NCName) in which the colon character (:) is not part of the name.  
  
-   You cannot define a namespace prefix two times.  
  
-   XML namespace prefixes and URIs are case-sensitive.  
  
-   The XML namespace prefix `xmlns` cannot be declared.  
  
-   The XML namespace prefix `xml` cannot be overridden with a namespace, other than the namespaces URI `'http://www.w3.org/XML/1998/namespace'`, and this URI that cannot be assigned a different prefix.  
  
-   The XML namespace prefix `xsi` cannot be redeclared when the ELEMENTS XSINIL directive is being used on the query.  

-   It is not necessary to declare the 'http://www.w3.org/2001/XMLSchema-instance' to use xsi standard namespace. It is implicitly added by the XML/XPATH processor if not specified and xpath expressions can use the xsi prefix as long as the 'http://www.w3.org/2001/XMLSchema-instance' schema is properly declared in the xml document.

-   URI string values are encoded according to the current database collation code page and are internally translated to Unicode.  
  
-   The XML namespace URI will be white-space collapsed following the XSD white-space collapse rules that are used for **xs:anyURI**. Also, note that no entitization or deentitization are performed on XML namespace URI values.  

-   The XML namespace URI will be checked for XML 1.0 characters that are not valid, and an error will be raised if one is found (such as, U+0007).  
  
-   The XML namespace URI (after all white space is collapsed) cannot be a zero-length string or an "invalid empty namespace URI" error occurs.  
  
-   The XMLNAMESPACES keyword is reserved in the context of the WITH clause.  
  
## Examples  
 For examples, see [Add Namespaces to Queries with WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
## See Also  
 [XQuery Language Reference &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
