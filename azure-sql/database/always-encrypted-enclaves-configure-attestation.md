---
title: "Configure attestation for Always Encrypted using Azure Attestation"
description: Configure Azure Attestation for Always Encrypted with secure enclaves in Azure SQL Database.
author: Pietervanhove
ms.author: pivanho
ms.reviewer: vanto
ms.date: 02/01/2023
ms.service: sql-database
ms.subservice: security
ms.topic: how-to
keywords:
  - "encrypt data"
  - "sql encryption"
  - "database encryption"
  - "sensitive data"
  - "Always Encrypted"
  - "secure enclaves"
  - "SGX"
  - "attestation"
---

# Configure attestation for Always Encrypted using Azure Attestation

[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

[Microsoft Azure Attestation](/azure/attestation/overview) is a solution for attesting Trusted Execution Environments (TEEs), including Intel Software Guard Extensions (Intel SGX) enclaves.

To use Azure Attestation for attesting Intel SGX enclaves used for [Always Encrypted with secure enclaves](/sql/relational-databases/security/encryption/always-encrypted-enclaves) in Azure SQL Database, you need to:

1. Create an [attestation provider](/azure/attestation/basic-concepts#attestation-provider) and configure it with the recommended attestation policy.

2. Determine the attestation URL and share it with application administrators.

> [!IMPORTANT]
>With Intel SGX enclaves in Azure SQL Database, attestation is mandatory and it requires Microsoft Azure Attestation.
VBS enclaves in Azure SQL Database (in preview) currently do not support attestation. This document only applies to Intel SGX enclaves.

> [!NOTE]
> Configuring attestation is the responsibility of the attestation administrator. See [Roles and responsibilities when configuring Intel SGX enclaves and attestation](always-encrypted-enclaves-plan.md#roles-and-responsibilities-when-configuring-intel-sgx-enclaves-and-attestation).

## Create and configure an attestation provider

An [attestation provider](/azure/attestation/basic-concepts#attestation-provider) is a resource in Azure Attestation that evaluates [attestation requests](/azure/attestation/basic-concepts#attestation-request) against [attestation policies](/azure/attestation/basic-concepts#attestation-request) and issues [attestation tokens](/azure/attestation/basic-concepts#attestation-token).

Attestation policies are specified using the [claim rule grammar](/azure/attestation/claim-rule-grammar).

> [!IMPORTANT]
> An attestation provider gets created with the default policy for Intel SGX enclaves, which does not validate the code running inside the enclave. Microsoft strongly advises you set the recommended policy used in the following output, and not use the default policy for Always Encrypted with secure enclaves.

Microsoft recommends the following policy for attesting Intel SGX enclaves used for Always Encrypted in Azure SQL Database:

```output
version= 1.0;
authorizationrules 
{
       [ type=="x-ms-sgx-is-debuggable", value==false ]
        && [ type=="x-ms-sgx-product-id", value==4639 ]
        && [ type=="x-ms-sgx-svn", value>= 2 ]
        && [ type=="x-ms-sgx-mrsigner", value=="e31c9e505f37a58de09335075fc8591254313eb20bb1a27e5443cc450b6e33e5"] 
    => permit();
};

```

The policy verifies:

- The enclave inside Azure SQL Database doesn't support debugging.
  
  Enclaves can be loaded with debugging disabled or enabled. Debugging support is designed to allow developers to troubleshoot the code running in an enclave. In a production system, debugging could enable an administrator to examine the content of the enclave, which would reduce the level of protection the enclave provides. The recommended policy disables debugging to ensure that if a malicious admin tries to turn on debugging support by taking over the enclave machine, attestation will fail.

- The product ID of the enclave matches the product ID assigned to Always Encrypted with secure enclaves.
  
  Each enclave has a unique product ID that differentiates the enclave from other enclaves. The product ID assigned to the Always Encrypted enclave is 4639.

- The security version number (SVN) of the library is greater than or equal to 2.
  
  The SVN allows Microsoft to respond to potential security bugs identified in the enclave code. In case a security issue is discovered and fixed, Microsoft will deploy a new version of the enclave with a new (incremented) SVN. The recommended policy is updated to reflect the new SVN. By updating your policy to match the recommended policy, you can ensure that if a malicious administrator tries to load an older and insecure enclave, attestation will fail.

- The library in the enclave has been signed using the Microsoft signing key (the value of the x-ms-sgx-mrsigner claim is the hash of the signing key).
  
  One of the main goals of attestation is to convince clients that the binary running in the enclave is the binary that is supposed to run. Attestation policies provide two mechanisms for this purpose. One is the **mrenclave** claim, which is the hash of the binary that is supposed to run in an enclave. The problem with the **mrenclave** is that the binary hash changes even with trivial changes to the code, which makes it hard to rev the code running in the enclave. Hence, we recommend the use of the **mrsigner**, which is a hash of a key that is used to sign the enclave binary. When Microsoft revs the enclave, the **mrsigner** stays the same as long as the signing key doesn't change. In this way, it becomes feasible to deploy updated binaries without breaking customers' applications.

> [!IMPORTANT]
> Microsoft may need to rotate the key used to sign the Always Encrypted enclave binary, which is expected to be a rare event. Before a new version of the enclave binary, signed with a new key, is deployed to Azure SQL Database, this article will be updated to provide a new recommended attestation policy and instructions on how you should update the policy in your attestation providers to ensure your applications continue to work uninterrupted.

For instructions for how to create an attestation provider and configure with an attestation policy using:

- [Quickstart: Set up Azure Attestation with Azure portal](/azure/attestation/quickstart-portal)
    > [!IMPORTANT]
    > When you configure your attestation policy with Azure portal, set Attestation Type to `SGX-IntelSDK`.
- [Quickstart: Set up Azure Attestation with Azure PowerShell](/azure/attestation/quickstart-powershell)
    > [!IMPORTANT]
    > When you configure your attestation policy with Azure PowerShell, set the `Tee` parameter to `SgxEnclave`.
- [Quickstart: Set up Azure Attestation with Azure CLI](/azure/attestation/quickstart-azure-cli)
    > [!IMPORTANT]
    > When you configure your attestation policy with Azure CLI, set the `attestation-type` parameter to `SGX-IntelSDK`.

## Determine the attestation URL for your attestation policy

After you've configured an attestation policy, you need to share the attestation URL with administrators of applications that use Always Encrypted with secure enclaves in Azure SQL Database. The attestation URL is the `Attest URI` of the attestation provider containing the attestation policy, which looks like this: `https://MyAttestationProvider.wus.attest.azure.net`.

### Use Azure portal to determine the attestation URL

In the Overview pane for your attestation provider, copy the value of the `Attest URI` property to clipboard.

### Use PowerShell to determine the attestation URL

Use the `Get-AzAttestation` cmdlet to retrieve the attestation provider properties, including AttestURI.

```powershell
Get-AzAttestation -Name $attestationProviderName -ResourceGroupName $attestationResourceGroupName
```

For more information, see [Create and manage an attestation provider](/azure/attestation/quickstart-powershell#create-and-manage-an-attestation-provider).

## Next steps

- [Manage keys for Always Encrypted with secure enclaves](/sql/relational-databases/security/encryption/always-encrypted-enclaves-manage-keys)

## See also

- [Getting started using Always Encrypted with secure enclaves](always-encrypted-enclaves-getting-started.md)
