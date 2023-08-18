---
title: Configure SQL Server to listen on a specific TCP port
description: Learn how to use SQL Server Configuration Manager to configure the Database Engine to listen on a specific fixed port other than the default port, 1433.
author: rwestMSFT
ms.author: randolphwest
ms.date: 03/30/2023
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "fixed port"
  - "static ports"
  - "ports [SQL Server], assigning numbers"
  - "assigning port numbers"
  - "dynamic ports [SQL Server]"
  - "TCP/IP [SQL Server], port numbers"
---
# Configure SQL Server to listen on a specific TCP port

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

This article describes how to configure an instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] to listen on a specific fixed port by using SQL Server Configuration Manager. If enabled, the default instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] listens on TCP port 1433. Named instances of the [!INCLUDE[ssDE](../../includes/ssde-md.md)] and [!INCLUDE[ssEW](../../includes/ssew-md.md)] are configured for [dynamic ports](../../tools/configuration-manager/tcp-ip-properties-ip-addresses-tab.md). This means they select an available port when the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service is started. When you connect to a named instance through a firewall, configure the [!INCLUDE[ssDE](../../includes/ssde-md.md)] to listen on a specific port, so that the appropriate port can be opened in the firewall.

Because port 1433 is the known standard for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], some organizations specify that the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] port number should be changed to enhance security. This might be helpful in some environments. However, the TCP/IP architecture permits a [port scanner](https://wikipedia.org/wiki/Port_scanner) to query for open ports, so changing the port number isn't considered a robust security measure.

For more information about the default Windows firewall settings, and a description of the TCP ports that affect the [!INCLUDE [ssde-md](../../includes/ssde-md.md)], Analysis Services, Reporting Services, and Integration Services, see [Configure the Windows Firewall to Allow SQL Server Access](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).

> [!TIP]  
> When selecting a port number, consult [https://www.iana.org/assignments/port-numbers](https://www.iana.org/assignments/port-numbers) for a list of port numbers that are assigned to specific applications. Select an unassigned port number. For more information, see [The default dynamic port range for TCP/IP has changed in Windows Vista and in Windows Server 2008](https://support.microsoft.com/kb/929851).

> [!WARNING]  
> The [!INCLUDE [ssde-md](../../includes/ssde-md.md)] begins listening on a new port when restarted. However the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service monitors the registry and reports the new port number as soon as the configuration is changed, even though the [!INCLUDE [ssde-md](../../includes/ssde-md.md)] might not be using it. Restart the [!INCLUDE [ssde-md](../../includes/ssde-md.md)] to ensure consistency and avoid connection failures.

## <a id="SSMSProcedure"></a> Use SQL Server Configuration Manager

#### Assign a TCP/IP port number to the SQL Server Database Engine

1. In SQL Server Configuration Manager, in the console pane, expand **SQL Server Network Configuration**, select **Protocols for \<instance name>**, and then in the right pane double-click **TCP/IP**.

   > [!NOTE]  
   >  If you are having trouble opening [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, see [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

1. In the **TCP/IP Properties** dialog box, on the **IP Addresses** tab, several IP addresses appear in the format **IP1**, **IP2**, up to **IPAll**. One of these is for the IP address of the loopback adapter, 127.0.0.1. Additional IP addresses appear for each IP address on the computer. (You may see both IP version 4 and IP version 6 addresses.) Right-click each address, and then select **Properties** to identify the IP address that you want to configure.

1. If the **TCP Dynamic Ports** dialog box contains **0**, indicating the [!INCLUDE[ssDE](../../includes/ssde-md.md)] is listening on dynamic ports, delete the 0.

   :::image type="content" source="media/configure-a-server-to-listen-on-a-specific-tcp-port/tcp-ports.png" alt-text="Screenshot showing the TCP ports.":::

1. In the **IP**_n_ **Properties** area box, in the **TCP Port** box, type the port number you want this IP address to listen on, and then select **OK**. Multiple ports may be specified by separating them with a comma. Select **OK**.

   > [!NOTE]  
   > If the **Listen All** setting on the **Protocol** tab is set to "Yes", then only **TCP Port** and **TCP Dynamic Port** values under the **IPAll** section will be used and individual **IP**_n_ sections will be ignored in their entirety. If the **Listen All** setting is set to "No", then the **TCP Port** and **TCP Dynamic Port** settings under the **IPAll** section will be ignored and the **TCP Port**, **TCP Dynamic Port**, and **Enabled** settings on the individual **IP**_n_ sections will be used instead.
   >
   > Each **IP**_n_ section has an **Enabled** setting with a default value of "No" which causes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to ignore this IP address even if it has a port defined.

1. In the console pane, select **SQL Server Services**.

1. In the details pane, right-click **SQL Server (**\<instance name>**)** and then select **Restart**, to stop and restart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## Connect

After you configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to listen on a specific port, there are three ways to connect to a specific port with a client application:

- Run the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser service on the server to connect to the [!INCLUDE[ssDE](../../includes/ssde-md.md)] instance by name.
- Create an alias on the client, specifying the port number.
- Program the client to connect using a custom connection string.

## See also

- [Create or Delete a Server Alias for Use by a Client (SQL Server Configuration Manager)](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)
- [SQL Server Browser Service](../../tools/configuration-manager/sql-server-browser-service.md)
