---
title: "Processing XML on the Client Side (SQLXML)"
description: Learn how to process XML on the client side by using the ClientSideXml property of the SqlXmlCommand object in the SQLXML Managed Classes.
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: xml
ms.topic: "reference"
helpviewer_keywords:
  - "processing XML on client side [SQLXML]"
  - "client-side XML formatting"
  - "Managed Classes [SQLXML], client-side XML formatting"
  - "SQLXML Managed Classes, client-side XML formatting"
  - "ClientSideXml property"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Processing XML on the Client Side (SQLXML Managed Classes)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  This example illustrates the use of the ClientSideXml property. The application executes a stored procedure on the server. The result of the stored procedure (a two-column rowset) is processed on the client side to produce an XML document.  
  
 The following GetContacts stored procedure returns **FirstName** and **LastName** of employees in the Person.Contact table in the AdventureWorks database.  
  
```  
USE AdventureWorks2022;
CREATE PROCEDURE GetContacts @LastName varchar(20)  
AS  
SELECT FirstName, LastName  
FROM   Person.Contact  
WHERE LastName = @LastName  
Go  
```  
  
 This C# application executes the stored procedure and specifies the FOR XML AUTO option in specifying the CommandText value. In the application, the ClientSideXml property of the SqlXmlCommand object is set to true. This allows you to execute preexisting stored procedures that return a rowset and apply an XML transformation to it on the client.  
  
> [!NOTE]  
>  In the code, you must provide the name of the instance of Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in the connection string.  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
    static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         //Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
         cmd.ClientSideXml = true;  
         cmd.CommandText = "EXEC GetContacts ? FOR XML NESTED";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         using (Stream strm = cmd.ExecuteStream())   
         {  
            using (StreamReader sr = new StreamReader(strm))  
                  {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         return 0;  
      }  
  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
 To test this example, you must have the [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework installed on your computer.  
  
### To test the application  
  
1.  Create the stored procedure.  
  
2.  Save the C# code (DocSample.cs) that is provided in this example in a folder. Edit the code to specify appropriate login and password information.  
  
3.  Compile the code. To compile the code at the command prompt, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     This creates an executable (DocSample.exe).  
  
4.  At the command prompt, execute DocSample.exe.  

