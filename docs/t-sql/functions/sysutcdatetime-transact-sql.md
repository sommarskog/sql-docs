---
title: "SYSUTCDATETIME (Transact-SQL)"
description: "SYSUTCDATETIME (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "12/01/2015"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "SYSUTCDATETIME"
  - "SYSUTCDATETIME_TSQL"
helpviewer_keywords:
  - "dates [SQL Server], functions"
  - "system time [SQL Server]"
  - "functions [SQL Server], date and time"
  - "time [SQL Server], functions"
  - "date and time [SQL Server], SYSUTCDATETIME"
  - "SYSUTCDATETIME function [SQL Server]"
  - "time [SQL Server], system"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current"
---
# SYSUTCDATETIME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Returns a **datetime2** value that contains the date and time of the computer on which the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is running. The date and time is returned as UTC time (Coordinated Universal Time). The fractional second precision specification has a range from 1 to 7 digits. The default precision is 7 digits.  
  
> [!NOTE]  
>  SYSDATETIME and SYSUTCDATETIME have more fractional seconds precision than GETDATE and GETUTCDATE. SYSDATETIMEOFFSET includes the system time zone offset. SYSDATETIME, SYSUTCDATETIME, and SYSDATETIMEOFFSET can be assigned to a variable of any one of the date and time types.  
  
 For an overview of all [!INCLUDE[tsql](../../includes/tsql-md.md)] date and time data types and functions, see [Date and Time Data Types and Functions](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
SYSUTCDATETIME ( )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Return Type  
 **datetime2**  
  
## Remarks  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] statements can refer to SYSUTCDATETIME anywhere they can refer to a **datetime2** expression.  
  
 SYSUTCDATETIME is a nondeterministic function. Views and expressions that reference this function in a column cannot be indexed.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] obtains the date and time values by using the GetSystemTimeAsFileTime() Windows API. The accuracy depends on the computer hardware and version of Windows on which the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is running. The precision of this API is fixed at 100 nanoseconds. The accuracy can be determined by using the GetSystemTimeAdjustment() Windows API.  
  
## Examples  
 The following examples use the six [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] system functions that return current date and time to return the date, time, or both. The values are returned in series; therefore, their fractional seconds might be different.  
  
### A. Showing the formats that are returned by the date and time functions  
 The following example shows the different formats that are returned by the date and time functions.  
  
```sql
SELECT SYSDATETIME() AS [SYSDATETIME()]  
    ,SYSDATETIMEOFFSET() AS [SYSDATETIMEOFFSET()]  
    ,SYSUTCDATETIME() AS [SYSUTCDATETIME()]  
    ,CURRENT_TIMESTAMP AS [CURRENT_TIMESTAMP]  
    ,GETDATE() AS [GETDATE()]  
    ,GETUTCDATE() AS [GETUTCDATE()];  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
SYSDATETIME()      2007-04-30 13:10:02.0474381
SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00
SYSUTCDATETIME()   2007-04-30 20:10:02.0474381
CURRENT_TIMESTAMP  2007-04-30 13:10:02.047
GETDATE()          2007-04-30 13:10:02.047
GETUTCDATE()       2007-04-30 20:10:02.047
```  
  
### B. Converting date and time to date  
 The following example shows you how to convert date and time values to `date`.  
  
```sql
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
2007-04-30
```  
  
### C. Converting date and time values to time  
 The following example shows you how to convert date and time values to `time`.  
  
 ```sql
DECLARE @DATETIME DATETIME = GetDate();
DECLARE @TIME TIME
SELECT @TIME = CONVERT(time, @DATETIME)
SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'
```
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Time             Date Time  
13:49:33.6330000 2009-04-22 13:49:33.633
```  
  
## See Also  
 [CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Date and Time Data Types and Functions &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  


