---
title: Custom Workflow XML Description
description: "Create a Custom Workflow - XML Description"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: "reference"
---
# Create a Custom Workflow - XML Description

[!INCLUDE [SQL Server Windows Only - ASDBMI](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], the [Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow*](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) method is called by SQL Server MDS Workflow Integration Service when a workflow starts. This method receives metadata and data about the item that triggered the workflow business rule as a block of XML. For example code that implements a workflow handler, see [Custom Workflow Example &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 The following example shows what the XML that is sent to the workflow handler might look like:  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 The following table describes some of the tags contained in this XML:  
  
|Tag|Description|  
|---------|-----------------|  
|\<Type>|The text you entered in the **Workflow type** text box in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] to identify which custom workflow assembly to load.|  
|\<SendData>|A Boolean value controlled by the **Include member data in the message** checkbox in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. A value of 1 means that the \<MemberData> section is sent; otherwise the \<MemberData> section is not sent.|  
|<Server_URL>|The text you entered in the **Workflow site** text box in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|<Action_ID>|The text you entered in the **Workflow name** text box in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|\<MemberData>|Contains the data of the member that triggered the workflow action. This is included only if the value of \<SendData> is 1.|  
|\<Enter*xxx*>|This set of tags contains metadata about the creation of the member, such as when it was created and who created it.|  
|\<LastChg*xxx*>|This set of tags contains metadata about the last change made to the member, such as when the change was made and who made it.|  
|\<Name>|The first attribute of the member that was changed. This example member contains only Name and Code attributes.|  
|\<Code>|The next attribute of the member that was changed. If this example member contained more attributes, they would follow this one.|  
  
## See Also  
 [Create a Custom Workflow &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [Custom Workflow Example &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
