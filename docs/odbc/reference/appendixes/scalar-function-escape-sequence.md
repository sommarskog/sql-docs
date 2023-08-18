---
title: "Scalar Function Escape Sequence"
description: "Scalar Function Escape Sequence"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "escape sequences [ODBC], scalar function"
  - "scalar functions [ODBC], escape sequences"
  - "ODBC escape sequences [ODBC], scalar function"
---
# Scalar Function Escape Sequence
ODBC uses escape sequences for scalar functions. The syntax of this escape sequence is as follows:  
  
```  
{fn scalar-function}  
```  
  
## Remarks  
 In BNF notation, the syntax is as follows:  
  
 *ODBC-scalar-function-escape* ::=  
  
 *ODBC-esc-initiator* fn *scalar-function ODBC-esc-terminator*  
  
 *scalar-function* ::= *function-name* (*argument-list*)  
  
 (The definitions for the nonterminals *function-name* and *function-name* (*argument-list*) are derived from the list of scalar functions in [Appendix E: Scalar Functions](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 To determine whether the data source supports procedures and the driver supports the ODBC procedure invocation syntax, an application can call **SQLGetInfo**. For more information, see [Appendix E: Scalar Functions](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
