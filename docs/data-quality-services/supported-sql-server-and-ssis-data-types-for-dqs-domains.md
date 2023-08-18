---
title: "Supported SQL Server and SSIS data types for DQS domains"
description: Describes the four data types for Data Quality Services (DQS) domains (Data, Decimal, Integer, and String) in SQL Server.
author: swinarko
ms.author: sawinark
ms.date: "11/08/2011"
ms.service: sql
ms.subservice: data-quality-services
ms.topic: conceptual
---
# Supported SQL Server and SSIS data types for DQS Domains

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sqlserver.md)]

  There are many data types in SQL Server and SQL Server Integration Services (SSIS), but only four data types for DQS domains: Date, Decimal, Integer, and String. Not all SQL Server and SSIS data types are supported in DQS. You can map your source data to a DQS domain for performing data-quality activities only if the source data type is supported in DQS, and matches with the DQS domain data type. This topic provides information about the SQL Server and SSIS data types that are supported, and available for mapping to each of the four domain data types in DQS.  
  
> [!NOTE]  
>  In .xlsx and .xls files, the data type of the source column is determined by the most prevalent data type in the first eight rows. If a cell does not conform to that data type, it will be given a null value. Similarly, in .csv files, the data type of the source column is determined by the most prevalent data type in the first eight rows.  
  
##  <a name="SQLServer"></a> Supported SQL Server Data Types 
 The following table provides information about the SQL Server data types supported for each DQS domain data type:  
  
|DQS Domain Data Type|Supported SQL Server Data Type|  
|--------------------------|------------------------------------|  
|Date|date|  
|Decimal|decimal<br /><br /> float<br /><br /> money<br /><br /> numeric<br /><br /> real<br /><br /> smallmoney|  
|Integer|bigint<br /><br /> int<br /><br /> smallint<br /><br /> tinyint|  
|String|char<br /><br /> nchar<br /><br /> nvarchar<br /><br /> varchar|  
  
 Rest of the SQL Server data types are not supported in DQS. For information about all the SQL Server data types, see [Data Types &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
##  <a name="SSIS"></a> Supported SSIS Data Types  
 The following table provides information about the SSIS data types supported for each DQS domain data type:  
  
|DQS Domain Data Type|Supported SSIS Data Type|  
|--------------------------|------------------------------|  
|Date|DT_DATE|  
|Decimal|DT_DECIMAL<br /><br /> DT_NUMERIC<br /><br /> DT_R4<br /><br /> DT_R8|  
|Integer|DT_I1<br /><br /> DT_I2<br /><br /> DT_I4<br /><br /> DT_I8<br /><br /> DT_U1<br /><br /> DT_U2<br /><br /> DT_U4<br /><br /> DT_U8|  
|String|DT_STR<br /><br /> DT_WSTR|  
  
 Rest of the SSIS data types are not supported in DQS. For information about all the SSIS data types, see [Integration Services Data Types](../integration-services/data-flow/integration-services-data-types.md).  
  
## See Also  
 [Managing a Domain](../data-quality-services/managing-a-domain.md)  
  
  
