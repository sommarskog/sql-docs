---
title: Troubleshoot Windows Authentication for Azure AD principals on Azure SQL Managed Instance
titleSuffix: Azure SQL Managed Instance
description: Learn to troubleshoot Azure Active Directory Kerberos authentication for Azure SQL Managed Instance.
author: sravanisaluru
ms.author: srsaluru
ms.reviewer: mathoma, bonova, urmilano, wiassaf, randolphwest
ms.date: 03/16/2023
ms.service: sql-managed-instance
ms.subservice: deployment-configuration
ms.topic: how-to
---
# Troubleshoot Windows Authentication for Azure AD principals on Azure SQL Managed Instance

This article contains troubleshooting steps for use when implementing [Windows Authentication for Azure AD principals](winauth-azuread-overview.md).

## Verify tickets are getting cached

Use the [klist](/windows-server/administration/windows-commands/klist) command to display a list of currently cached Kerberos tickets.

The `klist get krbtgt` command should return a ticket from the on-premises Active Directory realm.

```dos
klist get krbtgt/kerberos.microsoftonline.com
```

The `klist get MSSQLSvc` command should return a ticket from the `kerberos.microsoftonline.com` realm with a Service Principal Name (SPN) to `MSSQLSvc/<miname>.<dnszone>.database.windows.net:1433`.

```dos
klist get MSSQLSvc/<miname>.<dnszone>.database.windows.net:1433
```

The following are some well-known error codes:

- **0x6fb: SQL SPN not found** - Check that you've entered a valid SPN. If you've implemented the incoming trust-based authentication flow, revisit steps to [create and configure the Azure AD Kerberos Trusted Domain Object](winauth-azuread-setup-incoming-trust-based-flow.md#create-and-configure-the-azure-ad-kerberos-trusted-domain-object) to validate that you've performed all the configuration steps.

- **0x51f** - This error is likely related to a conflict with the Fiddler tool. To mitigate the issue, follow these steps:

  1. Run `netsh winhttp reset autoproxy`
  2. Run `netsh winhttp reset proxy`
  3. In the Windows registry, find `Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\iphlpsvc\Parameters\ProxyMgr` and delete any subentry that has a configuration with a port `:8888`
  4. Restart the machine and try again using Windows Authentication

- **0x52f** - Indicates that a referenced user name and authentication information are valid, but some user account restriction has prevented successful authentication. This can happen if you have an Azure AD conditional access policy configured. To mitigate the issue, you must exclude the Azure SQL Managed Instance Service Principal (named `<instance name> principal`) application in the CA rules.

## Investigate message flow failures

Use Wireshark, or the network traffic analyzer of your choice, to monitor traffic between the client and on-premises Kerberos Key Distribution Center (KDC).

When using Wireshark the following is expected:

- AS-REQ: Client => on-premises KDC => returns on-premises TGT.
- TGS-REQ: Client => on-premises KDC => returns referral to `kerberos.microsoftonline.com`.

## Next steps

Learn more about implementing Windows Authentication for Azure AD principals on Azure SQL Managed Instance:

- [What is Windows Authentication for Azure Active Directory principals on Azure SQL Managed Instance?](winauth-azuread-overview.md)
- [How to set up Windows Authentication for Azure SQL Managed Instance using Azure Active Directory and Kerberos](winauth-azuread-setup.md)
- [How Windows Authentication for Azure SQL Managed Instance is implemented with Azure Active Directory and Kerberos](winauth-implementation-aad-kerberos.md)
- [How to set up Windows Authentication for Azure Active Directory with the modern interactive flow](winauth-azuread-setup-modern-interactive-flow.md)
- [How to set up Windows Authentication for Azure AD with the incoming trust-based flow](winauth-azuread-setup-incoming-trust-based-flow.md)
