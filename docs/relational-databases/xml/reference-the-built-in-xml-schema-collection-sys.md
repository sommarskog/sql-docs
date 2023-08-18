---
title: "Reference the Built-in XML Schema Collection (sys)"
description: Learn how to reference the built-in XML schema collection sys that is predefined for every database you create.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 05/05/2022
ms.service: sql
ms.subservice: xml
ms.topic: conceptual
helpviewer_keywords:
  - "sys XML schema collections [SQL Server]"
  - "schema collections [SQL Server], predefined"
  - "predefined XML schema collections [SQL Server]"
  - "XML schema collections [SQL Server], predefined"
  - "built-in XML schema collections [SQL Server]"
---
# Reference the built-in XML schema collection (sys)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Every database you create has a predefined **sys** XML schema collection in the **sys** relational schema. It reserves these predefined schemas, and they can be accessed from any other user-created XML schema collection. The prefixes used in these predefined schemas are meaningful in XQuery. Only **xml** is a reserved prefix.

```xml
xml = http://www.w3.org/XML/1998/namespace
xs = http://www.w3.org/2001/XMLSchema
xsi = http://www.w3.org/2001/XMLSchema-instance
fn = http://www.w3.org/2004/07/xpath-functions
sqltypes = https://schemas.microsoft.com/sqlserver/2004/sqltypes
xdt = http://www.w3.org/2004/07/xpath-datatypes
(no prefix) = urn:schemas-microsoft-com:xml-sql
(no prefix) = https://schemas.microsoft.com/sqlserver/2004/SOAP
```

The **sqltypes** namespace contains components that can be referenced from any user-created XML schema collection. You can download the **sqltypes** schema from this [Microsoft Web site](https://go.microsoft.com/fwlink/?linkid=31850). The built-in components include the following:

- XSD types

- XML attributes **lang**, **base**, and **space**

- Components of the **sqltypes** namespace

The following query returns built-in components that can be referenced from a user-created XML schema collection:

```sql
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))
join sys.xml_schema_collections SC
on SC.xml_collection_id = C.xml_collection_id
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)
AND (SC.schema_id = 4));
GO
```

The following example shows how these components are referenced in a user schema. `CREATE XML SCHEMA COLLECTION` creates an XML schema collection that references the `varchar` type defined in the `sqltypes` namespace. The example also references the `lang` attribute that is defined in the `xml` namespace.

```sql
CREATE XML SCHEMA COLLECTION SC AS '
<schema
   xmlns="http://www.w3.org/2001/XMLSchema"
   targetNamespace="myNS"
   xmlns:ns="myNS"
   xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >
   <import namespace="http://www.w3.org/XML/1998/namespace"/>
   <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>
   <element name="root">
      <complexType>
          <sequence>
             <element name="a" type="string"/>
             <element name="b" type="string"/>
             <!-- varchar type is defined in the sys.sys collection and
                  can be referenced in any user-defined schema -->
             <element name="c" type="s:varchar"/>
          </sequence>
          <attribute name="att" type="int"/>
          <!-- xml:lang attribute is defined in the sys.sys collection
               and can be referenced in any user-defined schema -->
          <attribute ref="xml:lang"/>
      </complexType>
    </element>
</schema>';
GO
-- Cleanup
DROP xml schema collection SC;
GO
```

You should note the following:

- You can't modify XML schemas with these namespaces in any user-defined XML schema collection. For example, the following XML schema collection fails because it adds a component to the `sqltypes` protected namespace:

    ```sql
    CREATE XML SCHEMA COLLECTION SC AS '
    <schema xmlns="http://www.w3.org/2001/XMLSchema"
    targetNamespace
        ="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >
          <element name="root" type="string"/>
    </schema>';
    GO
    ```

- You can't use the `sys` XML schema collection to type `xml` columns, variables, or parameters. For example, the following code returns an error:

    ```sql
    DECLARE @x xml (sys.sys);
    ```

- Serialization of these built-in schemas isn't supported. For example, the following code returns an error:

    ```sql
    SELECT XML_SCHEMA_NAMESPACE(N'sys', N'sys')l
    GO
    ```

The following code is another example in which you create an XML schema collection that uses the `varchar` type defined in the `sqltypes` namespace:

```sql
CREATE XML SCHEMA COLLECTION SC AS '
<schema xmlns="http://www.w3.org/2001/XMLSchema"
        targetNamespace="myNS" xmlns:ns="myNS"
        xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">
   <import
     namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>
      <simpleType name="myType">
            <restriction base="s:varchar">
                  <maxLength value="20"/>
            </restriction>
      </simpleType>
      <element name="root" type="ns:myType"/>
</schema>';
GO
```

As shown in the following, you can create a typed `XML` variable, assign an XML instance to it, and verify that the value of the `<root>` element type is a `varchar` type.

```sql
DECLARE @var XML(SC);
SET @var = '<root xmlns="myNS">My data</root>'
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";
declare namespace ns="myNS";
data(/ns:root[1]) instance of sqltypes:varchar?');
GO
```

The `instance of sqltypes:varchar?` expression returns TRUE, because the `<root>` element value is of a type derived from **varchar** according to the schema that is associated with the `@var` variable.

## See also

- [XML Schema Collections &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)
