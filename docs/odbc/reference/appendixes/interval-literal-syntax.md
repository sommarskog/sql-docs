---
title: "Interval Literal Syntax"
description: "Interval Literal Syntax"
author: David-Engel
ms.author: v-davidengel
ms.date: "01/19/2017"
ms.service: sql
ms.subservice: connectivity
ms.topic: reference
helpviewer_keywords:
  - "literals [ODBC], interval"
  - "interval literals [ODBC]"
  - "ODBC literals [ODBC], interval"
---
# Interval Literal Syntax
The following syntax is used for interval literals in ODBC.  
  
 *interval-literal ::= INTERVAL* [+*&#124;*-] *interval-string interval-qualifier*  
  
 *interval-string* ::= *quote* { *year-month-literal* &#124; *day-time-literal* } *quote*  
  
 *year-month-literal* ::= *years-value* &#124; [*years-value* -] *months-value*  
  
 *day-time-literal* ::= *day-time-interval* &#124; *time-interval*  
  
 *day-time-interval* ::= *days-value* [*hours-value* [:*minutes-value*[:*seconds-value*]]]  
  
 *time-interval* ::= *hours-value* [:*minutes-value* [:*seconds-value* ] ]  
  
 &#124; *minutes-value* [:*seconds-value* ]  
  
 &#124; *seconds-value*  
  
 *years-value* ::= *datetime-value*  
  
 *months-value* ::= *datetime-value*  
  
 *days-value* ::= *datetime-value*  
  
 *hours-value* ::= *datetime-value*  
  
 *minutes-value* ::= *datetime-value*  
  
 *seconds-value* ::= *seconds-integer-value* [.[*seconds-fraction*] ]  
  
 *seconds-integer-value* ::= *unsigned-integer*  
  
 *seconds-fraction* ::= *unsigned-integer*  
  
 *datetime-value* ::= *unsigned-integer*  
  
 *interval-qualifier* ::= *start-field* TO *end-field* &#124; *single-datetime-field*  
  
 *start-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision* )]  
  
 *end-field* ::= *non-second-datetime-field* &#124; SECOND[(*interval-fractional-seconds-precision*)]  
  
 *single-datetime-field* ::= *non-second-datetime-field* [(*interval-leading-field-precision*)] &#124; SECOND[(*interval-leading-field-precision* [, (*interval-fractional-seconds-precision*)]  
  
 *datetime-field* ::= *non-second-datetime-field* &#124; SECOND  
  
 *non-second-datetime-field* ::= YEAR &#124; MONTH &#124; DAY &#124; HOUR &#124; MINUTE  
  
 *interval-fractional-seconds-precision* ::= *unsigned-integer*  
  
 *interval-leading-field-precision* ::= *unsigned-integer*  
  
 *quote* ::= '  
  
 *unsigned-integer* ::= *digit...*
