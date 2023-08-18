---
title: "Precision, scale, and length (Transact-SQL)"
description: "Precision is the number of digits in a number. Scale is the number of digits to the right of the decimal point in a number."
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: randolphwest
ms.date: 04/05/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: "reference"
helpviewer_keywords:
  - "data types [SQL Server], length"
  - "data types [SQL Server], scale"
  - "precision [SQL Server], data types"
  - "lengths [SQL Server], data types"
  - "number of digits"
  - "scale [SQL Server]"
  - "scale [SQL Server], data types"
  - "data types [SQL Server], precision"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# Precision, scale, and length (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Precision is the number of digits in a number. Scale is the number of digits to the right of the decimal point in a number. For example, the number `123.45` has a precision of `5` and a scale of `2`.

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], the default maximum precision of **numeric** and **decimal** data types is 38.

Length for a numeric data type is the number of bytes that are used to store the number. For **varchar** and **char**, the length of a character string is the number of bytes. For **nvarchar** and **nchar**, the length of the character string is the number of byte-pairs. The length for **binary**, **varbinary**, and **image** data types is the number of bytes. For example, an **int** data type can hold 10 digits, is stored in 4 bytes, and doesn't accept decimal points. The **int** data type has a precision of 10, a length of 4, and a scale of 0.

- When you concatenate two **char**, **varchar**, **binary**, or **varbinary** expressions, the length of the resulting expression is the sum of the lengths of the two source expressions, up to 8,000 bytes.

- When you concatenate two **nchar** or **nvarchar** expressions, the length of the resulting expression is the sum of the lengths of the two source expressions, up to 4,000 byte-pairs.

- When you compare two expressions of the same data type but different lengths by using `UNION`, `EXCEPT`, or `INTERSECT`, the resulting length is the longer of the two expressions.

## Remarks

The precision and scale of the numeric data types besides **decimal** are fixed. When an arithmetic operator has two expressions of the same type, the result has the same data type with the precision and scale defined for that type. If an operator has two expressions with different numeric data types, the rules of data type precedence define the data type of the result. The result has the precision and scale defined for its data type.

The following table defines how the precision and scale of the result are calculated when the result of an operation is of type **decimal**. The result is **decimal** when either:

- Both expressions are **decimal**.
- One expression is **decimal** and the other is a data type with a lower precedence than **decimal**.

The operand expressions are denoted as expression `e1`, with precision `p1` and scale `s1`, and expression `e2`, with precision `p2` and scale `s2`. The precision and scale for any expression that isn't **decimal** is the precision and scale defined for the data type of the expression. The function `max(a, b)` indicates to take the greater value of `a` or `b`. Similarly, `min(a, b)` indicates to take the smaller value of `a` or `b`.

| Operation | Result precision | Result scale <sup>1</sup> |
| --- | --- | --- |
| e1 + e2 | max(s1, s2) + max(p1 - s1, p2 - s2) + 1 | max(s1, s2) |
| e1 - e2 | max(s1, s2) + max(p1 - s1, p2 - s2) + 1 | max(s1, s2) |
| e1 * e2 | p1 + p2 + 1 | s1 + s2 |
| e1 / e2 | p1 - s1 + s2 + max(6, s1 + p2 + 1) | max(6, s1 + p2 + 1) |
| e1 { UNION &#124; EXCEPT &#124; INTERSECT } e2 | max(s1, s2) + max(p1 - s1, p2 - s2) | max(s1, s2) |
| e1 % e2 | min(p1 - s1, p2 - s2) + max(s1, s2) | max(s1, s2) |

<sup>1</sup> The result precision and scale have an absolute maximum of 38. When a result precision is greater than 38, it's reduced to 38, and the corresponding scale is reduced to try to prevent truncating the integral part of a result. In some cases such as multiplication or division, scale factor isn't reduced, to maintain decimal precision, although the overflow error can be raised.

In addition and subtraction operations, we need `max(p1 - s1, p2 - s2)` places to store the integral part of the decimal number. If there isn't enough space to store them (that is, `max(p1 - s1, p2 - s2) < min(38, precision) - scale`), the scale is reduced to provide enough space for the integral part. The resulting scale is `min(precision, 38) - max(p1 - s1, p2 - s2)`, so the fractional part might be rounded to fit into the resulting scale.

In multiplication and division operations, we need `precision - scale` places to store the integral part of the result. The scale might be reduced using the following rules:

1. The resulting scale is reduced to `min(scale, 38 - (precision-scale))` if the integral part is less than 32, because it can't be greater than `38 - (precision-scale)`. The result might be rounded in this case.
1. The scale isn't changed if it's less than 6 and if the integral part is greater than 32. In this case, an overflow error might be raised if it can't fit into **decimal(38, *scale*)**.
1. The scale is set to 6 if it's greater than 6 and if the integral part is greater than 32. In this case, both the integral part and scale would be reduced and resulting type is **decimal(38, 6)**. The result might be rounded to 6 decimal places, or the overflow error is thrown if the integral part can't fit into 32 digits.

## Examples

The following expression returns result `0.00000090000000000` without rounding, because the result can fit into **decimal(38, 17)**:

```sql
SELECT CAST(0.0000009000 AS DECIMAL(30, 20)) * CAST(1.0000000000 AS DECIMAL(30, 20)) [decimal(38, 17)];
```

In this case precision is `61`, and scale is `40`.

The integral part `(precision-scale = 21)` is less than 32, so this case is the first case in the multiplication rules, and scale is calculated as `min(scale, 38 - (precision-scale)) = min(40, 38 - (61-40)) = 17`. Result type is **decimal(38, 17)**.

The following expression returns result `0.000001` to fit into **decimal(38, 6)**:

```sql
SELECT CAST(0.0000009000 AS DECIMAL(30, 10)) * CAST(1.0000000000 AS DECIMAL(30, 10)) [decimal(38, 6)];
```

In this case precision is `61`, and scale is `20`.

Scale is greater than 6 and the integral part (`precision-scale = 41`) is greater than 32. This case is the third case in the multiplication rules, and the result type is **decimal(38, 6)**.

## See also

- [Expressions (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)
- [Data Types (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
