---
title: "Logging in the Script Task"
description: "Logging in the Script Task"
author: chugugrace
ms.author: chugu
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "reference"
helpviewer_keywords:
  - "SQL Server Integration Services packages, logs"
  - "SSIS packages, logs"
  - "logs [Integration Services], scripts"
  - "Integration Services packages, logs"
  - "Log method"
  - "SSIS Script task, logs"
  - "Script task [Integration Services], logs"
  - "packages [Integration Services], logs"
dev_langs:
  - "VB"
---
# Logging in the Script Task

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  The use of logging in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] packages lets you record detailed information about execution progress, results, and problems by recording predefined events or user-defined messages for later analysis. The Script task can use the <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> method of the **Dts** object to log user-defined data. If logging is enabled, and the **ScriptTaskLogEntry** event is selected for logging on the **Details** tab of the **Configure SSIS Logs** dialog box, a single call to the <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> method stores the event information in all the log providers configured for the task.  
  
> [!NOTE]  
>  Although you can perform logging directly from your Script task, you may want to consider implementing events rather than logging. When using events, not only can you enable the logging of event messages, but you can also respond to the event with default or user-defined event handlers.  
  
 For more information about logging, see [Integration Services &#40;SSIS&#41; Logging](../../../integration-services/performance/integration-services-ssis-logging.md).  
  
## Logging Example  
 The following example demonstrates logging from the Script task by logging a value that represents the number of rows processed.  
  
```vb  
Public Sub Main()  
  
    Dim rowsProcessed As Integer = 100  
    Dim emptyBytes(0) As Byte  
  
    Try  
        Dts.Log("Rows processed: " & rowsProcessed.ToString, _  
            0, _  
            emptyBytes)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Script Task Example", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
            //  
            int rowsProcessed = 100;  
            byte[] emptyBytes = new byte[0];  
  
            try  
            {  
                Dts.Log("Rows processed: " + rowsProcessed.ToString(), 0, emptyBytes);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                //An error occurred.  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
```  
  
 }  
  
## See Also  
 [Integration Services &#40;SSIS&#41; Logging](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
