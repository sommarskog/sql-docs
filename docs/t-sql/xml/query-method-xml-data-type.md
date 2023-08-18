---
title: query() Method (xml Data Type)
description: "query() Method (xml Data Type)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: 04/16/2020
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
helpviewer_keywords:
  - "query method"
  - "query() method"
dev_langs:
  - "TSQL"
---
# query() Method (xml Data Type)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Specifies an XQuery against an instance of the **xml** data type. The result is of **xml** type. The method returns an instance of untyped XML.  
  
## Syntax  
  
```syntaxsql
query ('XQuery')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
XQuery  
Is a string, an XQuery expression, that queries for XML nodes, such as elements and attributes, in an XML instance.  
  
## Examples  
This section provides examples of using the query() method of the **xml** data type.  
  
### A. Using the query() method against an xml type variable  
The following example declares a variable **\@myDoc** of **xml** type and assigns an XML instance to it. The **query()** method is then used to specify an XQuery against the document.  
  
The query retrieves the <`Features`> child element of the <`ProductDescription`> element:  
  
```sql
DECLARE @myDoc XML  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
The following output shows the result:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### B. Using the query() method against an XML type column  
In the following example, the **query()** method is used to specify an XQuery against the **CatalogDescription** column of **xml** type in the **AdventureWorks** database:  
  
```sql
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
Note the following items from the previous query:  
  
-   The CatalogDescription column is a typed **xml** column, which means it has a schema collection associated with it. In the [XQuery Prolog](../../xquery/modules-and-prologs-xquery-prolog.md), the **namespace** keyword defines the prefix that's later used in the query body.  
  
-   The **query()** method constructs XML, a <`Product`> element that has a **ProductModelID** attribute, in which the **ProductModelID** attribute value is retrieved from the database. For more information about XML construction, see [XML Construction &#40;XQuery&#41;](../../xquery/xml-construction-xquery.md).  
  
-   The [exist() method (XML data type)](../../t-sql/xml/exist-method-xml-data-type.md) in the WHERE clause finds only rows that contain the <`Warranty`> element in the XML. Again, the **namespace** keyword defines two namespace prefixes.  
  
The following output shows the partial result:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
Note the query() and exist() methods both declare the PD prefix. In these cases, you can use WITH XMLNAMESPACES to first define the prefixes and use it in the query.  
  
```sql
WITH XMLNAMESPACES 
(  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM
)  
SELECT CatalogDescription.query('<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />')
       AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/PD:ProductDescription/PD:Features/WM:Warranty ') = 1;
```  
  
## See Also  
 [Add Namespaces to Queries with WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Compare Typed XML to Untyped XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Create Instances of XML Data](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml Data Type Methods](../../t-sql/xml/xml-data-type-methods.md)   
 [XML Data Modification Language &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
