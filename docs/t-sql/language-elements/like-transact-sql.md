---
title: "LIKE (Transact-SQL)"
description: "Determines whether a specific character string matches a specified pattern."
author: rwestMSFT
ms.author: randolphwest
ms.date: 03/13/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ESCAPE"
  - "LIKE"
  - "ESCAPE_TSQL"
  - "LIKE_TSQL"
helpviewer_keywords:
  - "ESCAPE keyword"
  - "% (wildcard - character(s) to match)"
  - "ASCII pattern matching"
  - "pattern searching [SQL Server]"
  - "wildcard characters [SQL Server]"
  - "literals [SQL Server], using wildcards"
  - "character strings [SQL Server], LIKE"
  - "exact matches [SQL Server]"
  - "Boolean functions"
  - "LIKE comparisons"
  - "matching patterns [SQL Server]"
  - "NOT LIKE keyword"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current||=fabric"
---
# LIKE (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Determines whether a specific character string matches a specified pattern. A pattern can include regular characters and wildcard characters. During pattern matching, regular characters must exactly match the characters specified in the character string. However, wildcard characters can be matched with arbitrary fragments of the character string. Using wildcard characters makes the `LIKE` operator more flexible than using the `=` and `!=` string comparison operators. If any one of the arguments isn't of character string data type, the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] converts it to character string data type, if it's possible.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

Syntax for SQL Server and Azure SQL Database:

```syntaxsql
match_expression [ NOT ] LIKE pattern [ ESCAPE escape_character ]
```

Syntax for Azure Synapse Analytics and Parallel Data Warehouse:

```syntaxsql
match_expression [ NOT ] LIKE pattern
```

`ESCAPE` and `STRING_ESCAPE` are not supported in [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *match_expression*

Any valid [expression](../language-elements/expressions-transact-sql.md) of character data type.

#### *pattern*

The specific string of characters to search for in *match_expression*, and can include valid wildcard characters in the following table. *pattern* can be a maximum of 8,000 bytes.

If *match_expression* is a higher precedence data type than *pattern*, and the *pattern* length is greater than *match_expression*, you will get a truncation error during the implicit conversion of *pattern* value to *match_expression* type.

| Wildcard character | Description | Example |
| --- | --- | --- |
| `%` | Any string of zero or more characters. | `WHERE title LIKE '%computer%'` finds all book titles with the word `computer` anywhere in the book title. |
| `_` (underscore) | Any single character. | `WHERE au_fname LIKE '_ean'` finds all four-letter first names that end with `ean` (`Dean`, `Sean`, and so on). |
| `[ ]` | Any single character within the specified range `[a-f]` or set `[abcdef]`. | `WHERE au_lname LIKE '[C-P]arsen'` finds author last names ending with `arsen` and starting with any single character between `C` and `P`, for example `Carsen`, `Larsen`, `Karsen`, and so on. In range searches, the characters included in the range may vary depending on the sorting rules of the collation. |
| `[^]` | Any single character not within the specified range `[^a-f]` or set `[^abcdef]`. | `WHERE au_lname LIKE 'de[^l]%'` finds all author last names starting with `de` and where the following letter isn't `l`. |

#### *escape_character*

A character put in front of a wildcard character to indicate that the wildcard is interpreted as a regular character and not as a wildcard. *escape_character* is a character expression that has no default and must evaluate to only one character.

## Result type

**Boolean**

## Result value

`LIKE` returns TRUE if the *match_expression* matches the specified *pattern*.

## Remarks

When you do string comparisons by using `LIKE`, all characters in the pattern string are significant. Significant characters include any leading or trailing spaces. If a comparison in a query is to return all rows with a string `LIKE 'abc '` (`abc` followed by a single space), a row in which the value of that column is `abc` (`abc` without a space) isn't returned. However, trailing blanks, in the expression to which the pattern is matched, are ignored. If a comparison in a query is to return all rows with the string `LIKE 'abc'` (`abc` without a space), all rows that start with `abc` and have zero or more trailing blanks are returned.

A string comparison using a pattern that contains **char** and **varchar** data may not pass a `LIKE` comparison because of how the data is stored for each data type. The following example passes a local **char** variable to a stored procedure, and then uses pattern matching to find all employees whose last names start with the specified set of characters.

```sql
-- Uses AdventureWorks

CREATE PROCEDURE FindEmployee @EmpLName CHAR(20)
AS
SELECT @EmpLName = RTRIM(@EmpLName) + '%';

SELECT p.FirstName,
    p.LastName,
    a.City
FROM Person.Person p
INNER JOIN Person.Address a
    ON p.BusinessEntityID = a.AddressID
WHERE p.LastName LIKE @EmpLName;
GO

EXEC FindEmployee @EmpLName = 'Barb';
GO
```

In the `FindEmployee` procedure, no rows are returned because the **char** variable (`@EmpLName`) contains trailing blanks whenever the name contains fewer than 20 characters. Because the `LastName` column is **varchar**, there are no trailing blanks. This procedure fails because the trailing blanks are significant.

However, the following example succeeds because trailing blanks aren't added to a **varchar** variable.

```sql
-- Uses AdventureWorks
  
CREATE PROCEDURE FindEmployee @EmpLName VARCHAR(20)
AS
SELECT @EmpLName = RTRIM(@EmpLName) + '%';

SELECT p.FirstName,
    p.LastName,
    a.City
FROM Person.Person p
INNER JOIN Person.Address a
    ON p.BusinessEntityID = a.AddressID
WHERE p.LastName LIKE @EmpLName;
GO

EXEC FindEmployee @EmpLName = 'Barb';
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```output
FirstName      LastName            City
----------     -------------------- ---------------
Angela         Barbariol            Snohomish
David          Barber               Snohomish
(2 row(s) affected)
```

## Pattern match using LIKE

`LIKE` supports ASCII pattern matching and Unicode pattern matching. When all arguments (*match_expression*, *pattern*, and *escape_character*, if present) are ASCII character data types, ASCII pattern matching is performed. If any one of the arguments are of Unicode data type, all arguments are converted to Unicode, and Unicode pattern matching is performed. When you use Unicode data (**nchar** or **nvarchar** data types) with `LIKE`, trailing blanks are significant; however, for non-Unicode data, trailing blanks aren't significant. Unicode `LIKE` is compatible with the ISO standard. ASCII `LIKE` is compatible with earlier versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

The following series of examples shows the differences in rows returned between ASCII and Unicode `LIKE` pattern matching.

```sql
-- ASCII pattern matching with char column
CREATE TABLE t (col1 CHAR(30));

INSERT INTO t
VALUES ('Robert King');

SELECT * FROM t
WHERE col1 LIKE '% King'; -- returns 1 row

-- Unicode pattern matching with nchar column
CREATE TABLE t (col1 NCHAR(30));

INSERT INTO t
VALUES ('Robert King');

SELECT * FROM t
WHERE col1 LIKE '% King'; -- no rows returned

-- Unicode pattern matching with nchar column and RTRIM
CREATE TABLE t (col1 NCHAR(30));

INSERT INTO t
VALUES ('Robert King');

SELECT * FROM t
WHERE RTRIM(col1) LIKE '% King'; -- returns 1 row
```

> [!NOTE]  
> `LIKE` comparisons are affected by collation. For more information, see [COLLATE (Transact-SQL)](../statements/collations.md).

## Use the `%` wildcard character

If the `LIKE '5%'` symbol is specified, the [!INCLUDE[ssDE](../../includes/ssde-md.md)] searches for the number `5` followed by any string of zero or more characters.

For example, the following query shows all dynamic management views in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database, because they all start with the letters `dm`.

```sql
-- Uses AdventureWorks
  
SELECT Name
FROM sys.system_views
WHERE Name LIKE 'dm%';
GO
```

To see all objects that aren't dynamic management views, use `NOT LIKE 'dm%'`. If you have a total of 32 objects and `LIKE` finds 13 names that match the pattern, `NOT LIKE` finds the 19 objects that don't match the `LIKE` pattern.

You may not always find the same names with a pattern such as `LIKE '[^d][^m]%'`. Instead of 19 names, you may find only 14, with all the names that start with `d` or have `m` as the second letter eliminated from the results, and the dynamic management view names. This behavior is because match strings with negative wildcard characters are evaluated in steps, one wildcard at a time. If the match fails at any point in the evaluation, it's eliminated.

## Use wildcard characters as literals

 You can use the wildcard pattern matching characters as literal characters. To use a wildcard character as a literal character, enclose the wildcard character in brackets. The following table shows several examples of using the `LIKE` keyword and the `[ ]` wildcard characters.

| Symbol | Meaning |
| --- | --- |
| `LIKE '5[%]'` | `5%` |
| `LIKE '[_]n'` | `_n` |
| `LIKE '[a-cdf]'` | `a`, `b`, `c`, `d`, or `f` |
| `LIKE '[-acdf]'` | `-`, `a`, `c`, `d`, or `f` |
| `LIKE '[ [ ]'` | `[` |
| `LIKE ']'` | `]` |
| `LIKE 'abc[_]d%'` | `abc_d` and `abc_de` |
| `LIKE 'abc[def]'` | `abcd`, `abce`, and `abcf` |

## Pattern match with the ESCAPE clause

You can search for character strings that include one or more of the special wildcard characters. For example, the discounts table in a customers database may store discount values that include a percent sign (%). To search for the percent sign as a character instead of as a wildcard character, the ESCAPE keyword and escape character must be provided. For example, a sample database contains a column named comment that contains the text 30%. To search for any rows that contain the string 30% anywhere in the comment column, specify a WHERE clause such as `WHERE comment LIKE '%30!%%' ESCAPE '!'`. If ESCAPE and the escape character aren't specified, the [!INCLUDE[ssDE](../../includes/ssde-md.md)] returns any rows with the string `30!`.

If there is no character after an escape character in the LIKE pattern, the pattern isn't valid and the LIKE returns FALSE. If the character after an escape character isn't a wildcard character, the escape character is discarded and the following character is treated as a regular character in the pattern. These characters include the percent sign (%), underscore (_), and left bracket ([) wildcard characters when they are enclosed in double brackets ([ ]). Escape characters can be used within the double bracket characters ([ ]), including to escape a caret (^), hyphen (-), or right bracket (]).

`0x0000` (**char(0)**) is an undefined character in Windows collations, and can't be included in LIKE.

## Examples

### A. Use LIKE with the `%` wildcard character

 The following example finds all telephone numbers that have area code `415` in the `PersonPhone` table.

```sql
-- Uses AdventureWorks
  
SELECT p.FirstName,
    p.LastName,
    ph.PhoneNumber
FROM Person.PersonPhone AS ph
INNER JOIN Person.Person AS p
    ON ph.BusinessEntityID = p.BusinessEntityID
WHERE ph.PhoneNumber LIKE '415%'
ORDER BY p.LastName;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```output
FirstName             LastName             Phone
-----------------     -------------------  ------------
Ruben                 Alonso               415-555-124
Shelby                Cook                 415-555-0121
Karen                 Hu                   415-555-0114
John                  Long                 415-555-0147
David                 Long                 415-555-0123
Gilbert               Ma                   415-555-0138
Meredith              Moreno               415-555-0131
Alexandra             Nelson               415-555-0174
Taylor                Patterson            415-555-0170
Gabrielle              Russell             415-555-0197
Dalton                 Simmons             415-555-0115
(11 row(s) affected)
```

### B. Use NOT LIKE with the `%` wildcard character

The following example finds all telephone numbers in the `PersonPhone` table that have area codes other than `415`.

```sql
-- Uses AdventureWorks

SELECT p.FirstName,
    p.LastName,
    ph.PhoneNumber
FROM Person.PersonPhone AS ph
INNER JOIN Person.Person AS p
    ON ph.BusinessEntityID = p.BusinessEntityID
WHERE ph.PhoneNumber NOT LIKE '415%'
    AND p.FirstName = 'Gail'
ORDER BY p.LastName;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```output
FirstName              LastName            Phone
---------------------- -------------------- -------------------
Gail                  Alexander            1 (11) 500 555-0120
Gail                  Butler               1 (11) 500 555-0191
Gail                  Erickson             834-555-0132
Gail                  Erickson             849-555-0139
Gail                  Griffin              450-555-0171
Gail                  Moore                155-555-0169
Gail                  Russell              334-555-0170
Gail                  Westover             305-555-0100
(8 row(s) affected)
```

### C. Use the ESCAPE clause

The following example uses the `ESCAPE` clause and the escape character to find the exact character string `10-15%` in column `c1` of the `mytbl2` table.

```sql
USE tempdb;
GO

IF EXISTS (
        SELECT TABLE_NAME
        FROM INFORMATION_SCHEMA.TABLES
        WHERE TABLE_NAME = 'mytbl2'
        )
    DROP TABLE mytbl2;
GO

USE tempdb;
GO

CREATE TABLE mytbl2 (c1 SYSNAME);
GO

INSERT mytbl2
VALUES ('Discount is 10-15% off'),
    ('Discount is .10-.15 off');
GO

SELECT c1
FROM mytbl2
WHERE c1 LIKE '%10-15!% off%' ESCAPE '!';
GO
```

### D. Use the `[ ]` wildcard characters

The following example finds employees on the `Person` table with the first name of `Cheryl` or `Sheryl`.

```sql
-- Uses AdventureWorks

SELECT BusinessEntityID,
    FirstName,
    LastName
FROM Person.Person
WHERE FirstName LIKE '[CS]heryl';
GO
```

The following example finds the rows for employees in the `Person` table with last names of `Zheng` or `Zhang`.

```sql
-- Uses AdventureWorks
  
SELECT LastName,
    FirstName
FROM Person.Person
WHERE LastName LIKE 'Zh[ae]ng'
ORDER BY LastName ASC,
    FirstName ASC;
GO
```

## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

### E. Use LIKE with the `%` wildcard character

The following example finds all employees in the `DimEmployee` table with telephone numbers that start with `612`.

```sql
-- Uses AdventureWorks
  
SELECT FirstName,
    LastName,
    Phone
FROM DimEmployee
WHERE phone LIKE '612%'
ORDER BY LastName;
```

### F. Use NOT LIKE with the `%` wildcard character

The following example finds all telephone numbers in the `DimEmployee` table that don't start with `612`.

```sql
-- Uses AdventureWorks
  
SELECT FirstName,
    LastName,
    Phone
FROM DimEmployee
WHERE phone NOT LIKE '612%'
ORDER BY LastName;
```

### G. Use LIKE with the `_` wildcard character

The following example finds all telephone numbers that have an area code starting with `6` and ending in `2` in the `DimEmployee` table. The % wildcard character is included at the end of the search pattern to match all following characters in the phone column value.

```sql
-- Uses AdventureWorks
  
SELECT FirstName,
    LastName,
    Phone
FROM DimEmployee
WHERE phone LIKE '6_2%'
ORDER BY LastName;
```

## See also

- [PATINDEX (Transact-SQL)](../functions/patindex-transact-sql.md)
- [Expressions (Transact-SQL)](../language-elements/expressions-transact-sql.md)
- [What are the SQL database functions?](../functions/functions.md)
- [SELECT (Transact-SQL)](../queries/select-transact-sql.md)
- [SELECT (Transact-SQL)](../queries/select-transact-sql.md)
- [WHERE (Transact-SQL)](../queries/where-transact-sql.md)
