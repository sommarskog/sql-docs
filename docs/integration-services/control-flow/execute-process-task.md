---
title: "Execute Process Task"
description: "Execute Process Task"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.dts.designer.executeprocesstask.f1"
  - "sql13.dts.designer.executeprocesstask.general.f1"
  - "sql13.dts.designer.executeprocesstask.process.f1"
helpviewer_keywords:
  - "Execute Process task [Integration Services]"
---
# Execute Process Task

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  The Execute Process task runs an application or batch file as part of a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] package workflow. Although you can use the Execute Process task to open any standard application, such as [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] or [!INCLUDE[ofprword](../../includes/ofprword-md.md)], you typically use it to run business applications or batch files that work against a data source. For example, you can use the Execute Process task to expand a compressed text file. Then the package can use the text file as a data source for the data flow in the package. As another example, you can use the Execute Process task to run a custom [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] application that generates a daily sales report. Then you can attach the report to a Send Mail task and forward the report to a distribution list.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] includes other tasks that perform workflow operations such as executing packages. For more information, see [Execute Package Task](../../integration-services/control-flow/execute-package-task.md)  
  
## Custom Log Entries Available on the Execute Process Task  
 The following table lists the custom log entries for the Execute Process task. For more information, see [Integration Services &#40;SSIS&#41; Logging](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Log entry|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|Provides information about the process that the task is configured to run.<br /><br /> Two log entries are written. One contains information about the name and location of the executable that the task runs, and the other entry records the exit from the executable.|  
|**ExecuteProcessVariableRouting**|Provides information about which variables are routed to the input and outputs of the executable. Log entries are written for stdin (the input), stdout (the output), and stderr (the error output).|  
  
## Configuration of the Execute Process Task  
 You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer or programmatically.  
  
 For more information about how to set these properties in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, click the following topic:  
  
-   [Set the Properties of a Task or Container](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
### Property Settings  
 When the Execute Process task runs a custom application, the task provides input to the application through one or both of the following methods:  
  
-   A variable that you specify in the **StandardInputVariable** property setting. For more information about variables, see [Integration Services &#40;SSIS&#41; Variables](../../integration-services/integration-services-ssis-variables.md) and [Use Variables in Packages](../integration-services-ssis-variables.md).  
  
-   An argument that you specify in the **Arguments** property setting. (For example, if the task opens a document in Word, the argument can name the .doc file.)  
  
 To pass multiple arguments to a custom application in one Execute Process task, use spaces to delimit the arguments. An argument cannot include a space; otherwise, the task will not run. You can use an expression to pass a variable value as the argument. In the following example, the expression passes two variable values as arguments, and uses a space to delimit the arguments:  
  
 `@variable1 + " " + @variable2`  
  
 You can use an expression to set various Execute Process task properties.  
  
 When you use the **StandardInputVariable** property to configure the Execute Process task to provide input, call the **Console.ReadLine** method from the application to read the input. For more information, see [Console.ReadLine Method](/dotnet/api/system.console.readline)the topic, , in the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Class Library.  
  
 When you use the **Arguments** property to configure the Execute Process task to provide input, do one of the following steps to obtain the arguments:  
  
-   If you use Microsoft Visual Basic to write the application, set the **My.Application.CommandLineArgs** property. The following example sets the **My.Application.CommandLineArgs** property is to retrieve two arguments:  
  
    ```vb  
    Dim variable1 As String = My.Application.CommandLineArgs.Item(0)  
    Dim variable2 As String = My.Application.CommandLineArgs.Item(1)   
    ```  
  
     For more information, see the topic, [My.Application.CommandLineArgs Property](https://go.microsoft.com/fwlink/?LinkId=129200), in the [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] reference.  
  
-   If you use Microsoft Visual C# to write the application, use the **Main** method.  
  
     For more information, see the topic, [Command-Line Arguments (C# Programming Guide)](/dotnet/csharp/programming-guide/main-and-command-args/command-line-arguments), in the C# Programming Guide.  
  
 The Execute Process task also includes the **StandardOutputVariable** and **StandardErrorVariable** properties for specifying the variables that consume the standard output and error output of the application, respectively.  
  
 Additionally, you can configure the Execute Process task to specify a working directory, a time-out period, or a value to indicate that the executable ran successfully. The task can also be configured to fail if the return code of the executable does not match the value that indicates success, or if the executable is not found at the specified location.  
  
## Programmatic Configuration of the Execute Process Task  
 For more information about programmatically setting these properties, click the following topic:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteProcess.ExecuteProcess>  
  
## Execute Process Task Editor (General Page)
  Use the **General** pageof the **Execute Process Task Editor** dialog box to name and describe the Execute Process task.  
  
### Options  
 **Name**  
 Provide a unique name for the Execute Process task. This name is used as the label in the task icon.  
  
> [!NOTE]  
>  Task names must be unique within a package.  
  
 **Description**  
 Type a description of the Execute Process task.  
  
## Execute Process Task Editor (Process Page)
  Use the **Process** page of the **Execute Process Task Editor** dialog box to configure the options that execute the process. These options include the executable to run, its location, command prompt arguments, and the variables that provide input and capture output.  
  
### Options  
 **RequireFullFileName**  
 Indicate whether the task should fail if the executable is not found at the specified location.  
  
 **Executable**  
 Type the name of the executable to run.  
  
 **Arguments**  
 Provide command prompt arguments.  
  
 **WorkingDirectory**  
 Type the path of the folder that contains the executable, or click the browse button **(...)** and locate the folder.  
  
 **StandardInputVariable**  
 Select a variable to provide the input to the process, or click \<**New variable...**> to create a new variable:  
  
 **Related Topics:** [Add Variable](../integration-services-ssis-variables.md)  
  
 **StandardOutputVariable**  
 Select a variable to capture the output of the process, or click \<**New variable...**> to create a new variable.  
  
 **StandardErrorVariable**  
 Select a variable to capture the error output of the processor, or click \<**New variable...**> to create a new variable.  
  
 **FailTaskIfReturnCodeIsNotSuccessValue**  
 Indicate whether the task fails if the process exit code is different from the value specified in **SuccessValue**.  
  
 **SuccessValue**  
 Specify the value returned by the executable to indicate success. By default this value is set to **0**.  
  
 **TimeOut**  
 Specify the number of seconds that the process can run. A value of **0** indicates that no time-out value is used, and the process runs until it is completed or until an error occurs.  
  
 **TerminateProcessAfterTimeOut**  
 Indicate whether the process is forced to end after the time-out period specified by the **TimeOut** option. This option is available only if **TimeOut** is not **0**.  
  
 **WindowStyle**  
 Specify the window style in which to run the process.  
  
## See Also  
 [Integration Services Tasks](../../integration-services/control-flow/integration-services-tasks.md)   
 [Control Flow](../../integration-services/control-flow/control-flow.md)  
  
