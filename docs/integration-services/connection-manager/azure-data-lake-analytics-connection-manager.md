---
title: "Azure Data Lake Analytics connection manager"
description: A SQL Server Integration Services (SSIS) package can use the Azure Data Lake Analytics connection manager to connect to a Data Lake Analytics account.
author: "yanancai"
ms.author: "yanacai"
ms.reviewer: maghan
ms.date: "05/18/2018"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "SQL13.DTS.DESIGNER.AFPADLSCM.F1"
  - "sql14.dts.designer.afpadlscm.f1"
---
# Azure Data Lake Analytics connection manager

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



A SQL Server Integration Services (SSIS) package can use the Azure Data Lake Analytics connection manager to connect to a Data Lake Analytics account with one of the two following authentication types:
-   Azure Active Directory (Azure AD) User Identity
-   Azure AD Service Identity 

The Data Lake Analytics connection manager is a component of the [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
## Configure the connection manager

1. In the **Add SSIS Connection Manager** dialog box, select **AzureDataLakeAnalytics** > **Add**. The **Azure Data Lake Analytics Connection Manager Editor** dialog box opens.
  
2. In the **Azure Data Lake Analytics Connection Manager Editor** dialog box, in the **ADLA Account Name** field, provide the Data Lake Analytics account name. For example: myadlaaccountname.
  
3. In the **Authentication** field, choose the appropriate authentication type to access the data in Data Lake Analytics.

   a. If you select the **Azure AD User Identity** authentication option:
   
      i. Provide values for the **User Name** and **Password** fields.    
      ii. To test the connection, select **Test Connection**. If you or the tenant administrator didn't previously consent to allow SSIS to access your Data Lake Analytics account, select **Accept** when prompted. For more information about this consent experience, see [Integrating applications with Azure Active Directory](/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad).
    
   > [!NOTE] 
   > When you select the **Azure AD User Identity** authentication option, multi-factor authentication and Microsoft account authentication are not supported.
    
   b. If you select the **Azure AD Service Identity** authentication option:
   
      i. Create an Azure AD application and service principal to access the Data Lake Analytics account. For more information about this authentication option, see [Use portal to create Active Directory application and service principal that can access resources](/azure/azure-resource-manager/resource-group-create-service-principal-portal).    
      ii. Assign appropriate permissions to let this Azure AD application access your Data Lake Analytics account. Learn how to grant permissions to your Data Lake Analytics account by using the [Add User wizard](/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user).    
      iii. Provide values for the **Application ID**, **Authentication Key**, and **Tenant ID** fields.    
      iv. To test the connection, select **Test Connection**.  

4. Select **OK** to close the **Azure Data Lake Analytics Connection Manager Editor** dialog box.  

## View the properties of the connection manager
You can see the properties of the connection manager you created in the **Properties** window.  
  
