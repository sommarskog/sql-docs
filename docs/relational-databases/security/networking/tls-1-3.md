---
title: TLS 1.3 support
description: This article discusses TLS 1.3 support with SQL Server 2022
author: srdan-bozovic-msft
ms.author: srbozovi
ms.date: 06/30/2023
ms.service: sql
ms.subservice: security
ms.topic: conceptual
monikerRange: ">= sql-server-ver16||>= sql-server-linux-ver16"
---
# TLS 1.3 support

[!INCLUDE [SQL Server 2022](../../../includes/applies-to-version/sqlserver2022.md)]

[!INCLUDE [sssql22-md](../../../includes/sssql22-md.md)] supports Transport Layer Security (TLS) 1.3 when TDS 8.0 is used.

## Differences between TLS 1.2 and TLS 1.3

TLS 1.3 reduces the number of round trips from two to one during the handshake phase, making it faster and more secure than TLS 1.2. The server hello packet containing server certificate is encrypted and one Round Trip Time (1-RTT) resumption is discontinued, and replaced with 0-RTT resumption based on client key share. Added security of TLS 1.3 comes from discontinuing certain cyphers and algorithms.

Here's a list of algorithms and ciphers removed in TLS 1.3:

- RC4 stream cipher
- RSA key exchange
- SHA-1 hash function
- CBC (block) mode ciphers
- MD5 algorithm
- Various non-ephemeral Diffie-Hellman groups
- EXPORT-strength ciphers
- DES
- 3DES

## Next steps

- [Connect to SQL Server with strict encryption](connect-with-strict-encryption.md)
