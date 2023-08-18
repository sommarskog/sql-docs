---
title: "Date and time data"
description: "Describes how to use the new date and time data types introduced in SQL Server 2008."
author: David-Engel
ms.author: v-davidengel
ms.reviewer: v-kaywon
ms.date: "09/30/2019"
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
dev_langs:
  - "csharp"
---
# Date and time data

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008 introduces new data types for handling date and time information. The new data types include separate types for date and time, and expanded data types with greater range, precision, and time-zone awareness. The Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) provides full support for all the new features of the SQL Server 2008 Database Engine. You must install the .NET Framework 3.5 SP1 (or later) or .NET Core 1.0 (or later) to use these new features with SqlClient.  
  
Versions of SQL Server earlier than SQL Server 2008 only had two data types for working with date and time values: `datetime` and `smalldatetime`. Both of these data types contain both the date value and a time value, which makes it difficult to work with only date or only time values. Also, these data types only support dates that occur after the introduction of the Gregorian calendar in England in 1753. Another limitation is that these older data types are not time-zone aware, which makes it difficult to work with data that originates from multiple time zones.  
  
Complete documentation for SQL Server data types is available in SQL Server Books Online. See [Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100)) for entry-level topics on date and time data.
  
## Date/Time data types introduced in SQL Server 2008  
 The following table describes the new date and time data types.  
  
|SQL Server data type|Description|  
|--------------------------|-----------------|  
|`date`|The `date` data type has a range of January 1, 01 through December 31, 9999 with an accuracy of 1 day. The default value is January 1, 1900. The storage size is 3 bytes.|  
|`time`|The `time` data type stores time values only, based on a 24-hour clock. The `time` data type has a range of 00:00:00.0000000 through 23:59:59.9999999 with an accuracy of 100 nanoseconds. The default value is 00:00:00.0000000 (midnight). The `time` data type supports user-defined fractional second precision, and the storage size varies from 3 to 6 bytes, based on the precision specified.|  
|`datetime2`|The `datetime2` data type combines the range and precision of the `date` and `time` data types into a single data type.<br /><br /> The default values and string literal formats are the same as those defined in the `date` and `time` data types.|  
|`datetimeoffset`|The `datetimeoffset` data type has all the features of `datetime2` with an additional time zone offset. The time zone offset is represented as [+&#124;-] HH:MM. HH is 2 digits ranging from 00 to 14 that represent the number of hours in the time zone offset. MM is 2 digits ranging from 00 to 59 that represent the number of additional minutes in the time zone offset. Time formats are supported to 100 nanoseconds. The mandatory + or - sign indicates whether the time zone offset is added or subtracted from UTC (Universal Time Coordinate or Greenwich Mean Time) to obtain the local time.|  
  
> [!NOTE]
>  For more information about using the `Type System Version` keyword, see <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## Date format and date order  
How SQL Server parses date and time values depends not only on the type system version and server version, but also on the server's default language and format settings. A date string that works for the date formats of one language might be unrecognizable if the query is executed by a connection that uses a different language and date format setting.  
  
The Transact-SQL SET LANGUAGE statement implicitly sets the DATEFORMAT that determines the order of the date parts. You can use the SET DATEFORMAT Transact-SQL statement on a connection to disambiguate date values by ordering the date parts in MDY, DMY, YMD, YDM, MYD, or DYM order.  
  
If you do not specify any DATEFORMAT for the connection, SQL Server uses the default language associated with the connection. For example, a date string of '01/02/03' would be interpreted as MDY (January 2, 2003) on a server with a language setting of United States English, and as DMY (February 1, 2003) on a server with a language setting of British English. The year is determined by using SQL Server's cutoff year rule, which defines the cutoff date for assigning the century value. For more information, see [two digit year cutoff Option](/previous-versions/sql/sql-server-2008-r2/ms189577(v=sql.105)) in SQL Server Books Online.  
  
> [!NOTE]
>  The YDM date format is not supported when converting from a string format to `date`, `time`, `datetime2`, or `datetimeoffset`.  
  
For more information about how SQL Server interprets date and time data, see [Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100)) in SQL Server 2008 Books Online.  
  
## Date/Time data types and parameters  
The following enumerations have been added to <xref:System.Data.SqlDbType> to support the new date and time data types.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

You can specify the data type of a <xref:Microsoft.Data.SqlClient.SqlParameter> by using one of the preceding <xref:System.Data.SqlDbType> enumerations. 

> [!NOTE]
> You cannot set the `DbType` property of a `SqlParameter` to `SqlDbType.Date`.

You can also specify the type of a <xref:Microsoft.Data.SqlClient.SqlParameter> generically by setting the <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> property of a `SqlParameter` object to a particular <xref:System.Data.DbType> enumeration value. The following enumeration values have been added to <xref:System.Data.DbType> to support the `datetime2` and `datetimeoffset` data types:  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
These new enumerations supplement the `Date`, `Time`, and `DateTime` enumerations.  
  
The Microsoft SqlClient Data Provider type of a parameter object is inferred from the .NET type of the value of the parameter object, or from the `DbType` of the parameter object. No new <xref:System.Data.SqlTypes> data types have been introduced to support the new date and time data types. The following table describes the mappings between the SQL Server 2008 date and time data types and the CLR data types.  
  
|SQL Server data type|.NET type|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### SqlParameter properties  
 The following table describes `SqlParameter` properties that are relevant to date and time data types.  
  
|Property|Description|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|Gets or sets whether a value is nullable. When you send a null parameter value to the server, you must specify <xref:System.DBNull>, rather than `null` (`Nothing` in Visual Basic). For more information about database nulls, see [Handling null values](handle-null-values.md).|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|Gets or sets the maximum number of digits used to represent the value. This setting is ignored for date and time data types.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|Gets or sets the number of decimal places to which the time portion of the value is resolved for `Time`, `DateTime2`,and `DateTimeOffset`. The default value is 0, which means that the actual scale is inferred from the value and sent to the server.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Ignored for date and time data types.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Gets or sets the parameter value.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Gets or sets the parameter value.|  
  
> [!NOTE]
>  Time values that are less than zero or greater than or equal to 24 hours will throw an <xref:System.ArgumentException>.  
  
### Creating parameters  
You can create a <xref:Microsoft.Data.SqlClient.SqlParameter> object by using its constructor, or by adding it to a <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> collection by calling the `Add` method of the <xref:Microsoft.Data.SqlClient.SqlParameterCollection>. The `Add` method will take as input either constructor arguments or an existing parameter object.  
  
The next sections in this topic provide examples of how to specify date and time parameters.
  
### Date example  
The following code fragment demonstrates how to specify a `date` parameter.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### Time example  
The following code fragment demonstrates how to specify a `time` parameter.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### Datetime2 example  
The following code fragment demonstrates how to specify a `datetime2` parameter with both the date and time parts.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### DateTimeOffSet example  
The following code fragment demonstrates how to specify a `DateTimeOffSet` parameter with a date, a time, and a time zone offset of 0.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### AddWithValue  
You can also supply parameters by using the `AddWithValue` method of a <xref:Microsoft.Data.SqlClient.SqlCommand>, as shown in the following code fragment. However, the `AddWithValue` method does not allow you to specify the <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> or <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> for the parameter.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
The `@date` parameter could map to a `date`, `datetime`, or `datetime2` data type on the server. When working with the new `datetime` data types, you must explicitly set the parameter's <xref:System.Data.SqlDbType> property to the data type of the instance. Using <xref:System.Data.SqlDbType.Variant> or implicitly supplying parameter values can cause problems with backward compatibility with the `datetime` and `smalldatetime` data types.  
  
The following table shows which `SqlDbTypes` are inferred from which CLR types:  
  
|CLR type|Inferred SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## Retrieving date and time data  
The following table describes methods that are used to retrieve SQL Server 2008 date and time values.  
  
|SqlClient method|Description|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|Retrieves the specified column value as a <xref:System.DateTime> structure.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|Retrieves the specified column value as a <xref:System.DateTimeOffset> structure.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|Returns the type that is the underlying provider-specific type for the field. Returns the same types as `GetFieldType` for new date and time types.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|Retrieves the value of the specified column. Returns the same types as `GetValue` for the new date and time types.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|Retrieves the values in the specified array.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|Retrieves the column value as a <xref:System.Data.SqlTypes.SqlString>. An <xref:System.InvalidCastException> occurs if the data cannot be expressed as a `SqlString`.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|Retrieves column data as its default `SqlDbType`. Returns the same types as `GetValue` for the new date and time types.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|Retrieves the values in the specified array.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Retrieves the column value as a string if the Type System Version is set to SQL Server 2005. An <xref:System.InvalidCastException> occurs if the data cannot be expressed as a string.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|Retrieves the specified column value as a <xref:System.TimeSpan> structure.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|Retrieves the specified column value as its underlying CLR type.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|Retrieves column values in an array.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|Returns a <xref:System.Data.DataTable> that describes the metadata of the result set.|  
  
> [!NOTE]
>  The new date and time `SqlDbTypes` are not supported for code that is executing in-process in SQL Server. An exception will be raised if one of these types is passed to the server.  
  
## Specifying date and time values as literals  
You can specify date and time data types by using a variety of different literal string formats, which SQL Server then evaluates at run time, converting them to internal date/time structures. SQL Server recognizes date and time data that is enclosed in single quotation marks ('). The following examples demonstrate some formats:  
  
- Alphabetic date formats, such as `'October 15, 2006'`.  
  
- Numeric date formats, such as `'10/15/2006'`.  
  
- Unseparated string formats, such as `'20061015'`, which would be interpreted as October 15, 2006 if you are using the ISO standard date format.  
  
> [!NOTE]
>  You can find complete documentation for all of the literal string formats and other features of the date and time data types in SQL Server Books Online.  
  
Time values that are less than zero or greater than or equal to 24 hours will throw an <xref:System.ArgumentException>.  
  
## Resources in SQL Server 2008 Books Online  
For more information about working with date and time values in SQL Server 2008, see the following resources in SQL Server 2008 Books Online.  
  
|Topic|Description|  
|-----------|-----------------|  
|[Date and Time Data Types and Functions (Transact-SQL)](/previous-versions/sql/sql-server-2008/ms186724(v=sql.100))|Provides an overview of all Transact-SQL date and time data types and functions.|  
|[Using Date and Time Data](/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))|Provides information about the date and time data types and functions, and examples of using them.|  
|[Data Types (Transact-SQL)](/previous-versions/sql/sql-server-2008/ms187752(v=sql.100))|Describes system data types in SQL Server 2008.|  
  
## Next steps
- [SQL Server data types and ADO.NET](sql-server-data-types.md)