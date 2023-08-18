---
title: SQL Server connection pooling
description: Learn how Microsoft SqlClient Data Provider for SQL Server minimizes the cost of opening connections by using SQL Server connection pooling, which reduces overhead for new connections.
author: David-Engel
ms.author: v-davidengel
ms.date: 03/07/2023
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
dev_langs:
  - "csharp"
---
# SQL Server connection pooling (ADO.NET)

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Connecting to a database server typically consists of several time-consuming steps. A physical channel such as a socket or a named pipe must be established, the initial handshake with the server must occur, the connection string information must be parsed, the connection must be authenticated by the server, checks must be run for enlisting in the current transaction, and so on.

In practice, most applications use only one or a few different configurations for connections. This means that during application execution, many identical connections will be repeatedly opened and closed. To minimize the cost of opening connections, Microsoft SqlClient Data Provider for SQL Server uses an optimization technique called *connection pooling*.

Connection pooling reduces the number of times that new connections must be opened. The *pooler* maintains ownership of the physical connection. It manages connections by keeping alive a set of active connections for each given connection configuration. Whenever a user calls `Open` on a connection, the pooler looks for an available connection in the pool. If a pooled connection is available, it returns it to the caller instead of opening a new connection. When the application calls `Close` on the connection, the pooler returns it to the pooled set of active connections instead of closing it. Once the connection is returned to the pool, it is ready to be reused on the next `Open` call.

Only connections with the same configuration can be pooled. Microsoft SqlClient Data Provider for SQL Server keeps several pools at the same time, one for each configuration. Connections are separated into pools by connection string, and by Windows identity when integrated security is used. Connections are also pooled based on whether they are enlisted in a transaction. When using <xref:Microsoft.Data.SqlClient.SqlConnection.ChangePassword%2A>, the <xref:Microsoft.Data.SqlClient.SqlCredential> instance affects the connection pool. Different instances of <xref:Microsoft.Data.SqlClient.SqlCredential> will use different connection pools, even if the user ID and password are the same.

Pooling connections can significantly enhance the performance and scalability of your application. By default, connection pooling is enabled in the Microsoft SqlClient Data Provider for SQL Server. Unless you explicitly disable it, the pooler optimizes the connections as they are opened and closed in your application. You can also supply several connection string modifiers to control connection pooling behavior. For more information, see "**Controlling Connection Pooling with Connection String Keywords**" later in this topic.

> [!IMPORTANT]
> When connection pooling is enabled, and if a timeout error or other login error occurs, an exception will be thrown and subsequent connection attempts will fail for the next **5** seconds, the "`blocking period`". If the application attempts to connect within the blocking period, the first exception will be thrown again. Subsequent failures after a blocking period ends will result in a new blocking periods that is twice as long as the previous blocking period, up to a *maximum of **1** minute*.

> [!NOTE]
> The "`blocking period`" mechanism doesn't apply to Azure SQL Server by default. This behavior can be changed by modifying the <xref:Microsoft.Data.SqlClient.PoolBlockingPeriod> property in <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString> except for *.NET Standard*.

## Pool creation and assignment

When a connection is first opened, a connection pool is created based on an exact matching algorithm that associates the pool with the connection string in the connection. Each connection pool is associated with a distinct connection string. When a new connection is opened, if the connection string is not an exact match to an existing pool, a new pool is created.

> [!NOTE]
> Connections are pooled per _process_, per _application domain_, per _connection string_ and when integrated security is used, per _Windows identity_. Connection strings must also be an exact match; keywords supplied in a different order for the same connection will be pooled separately.

> [!NOTE]
> If `MinPoolSize` is either not specified in the connection string or is specified as zero, the connections in the pool will be closed after a period of inactivity. However, if the specified `MinPoolSize` is greater than zero, the connection pool is not destroyed until the `AppDomain` is unloaded and the process ends. Maintenance of inactive or empty pools involves minimal system overhead.

> [!NOTE]
> The pool is automatically cleared when a fatal error occurs, such as a failover.

In the following C# example, three new <xref:Microsoft.Data.SqlClient.SqlConnection> objects are created, but only two connection pools are required to manage them. Note that the first and second connection strings differ by the value assigned for `Initial Catalog`.  


[!code-csharp[SqlConnection_Pooling#1](~/../sqlclient/doc/samples/SqlConnection_Pooling.cs#1)]

## Add connections

A connection pool is created for each unique connection string. When a pool is created, multiple connection objects are created and added to the pool so that the minimum pool size requirement is satisfied. Connections are added to the pool as needed, up to the maximum pool size specified (**100 is the default**). Connections are released back into the pool when they are closed or disposed.

When a <xref:Microsoft.Data.SqlClient.SqlConnection> object is requested, it is obtained from the pool if a usable connection is available. To be usable, a connection must be unused, have a matching transaction context or be unassociated with any transaction context, and have a valid link to the server.

The connection pooler satisfies requests for connections by reallocating connections as they are released back into the pool. If the maximum pool size has been reached and no usable connection is available, the request is queued. The pooler then tries to reclaim any connections until the time-out is reached (**the default is 15 seconds**). If the pooler cannot satisfy the request before the connection times out, an exception is thrown.

> [!CAUTION]
> We strongly recommend that you always close the connection when you are finished using it so that the connection will be returned to the pool. You can do this using either the `Close` or `Dispose` methods of the `Connection` object, or by opening all connections inside a `using` statement in C#, or a `Using` statement in Visual Basic. Connections that are not explicitly closed might not be added or returned to the pool. For more information, see [using Statement](/dotnet/csharp/language-reference/keywords/using-statement) or [How to: Dispose of a System Resource](/dotnet/visual-basic/programming-guide/language-features/control-flow/how-to-dispose-of-a-system-resource) for Visual Basic.

> [!NOTE]
> Do not call `Close` or `Dispose` on a `Connection`, a `DataReader`, or any other managed object in the `Finalize` method of your class. In a finalizer, only release unmanaged resources that your class owns directly. If your class does not own any unmanaged resources, do not include a `Finalize` method in your class definition. For more information, see [Garbage Collection](/dotnet/standard/garbage-collection/index).

For more info about the events associated with opening and closing connections, see [Audit Login Event Class](../../relational-databases/event-classes/audit-login-event-class.md) and [Audit Logout Event Class](../../relational-databases/event-classes/audit-logout-event-class.md) in the SQL Server documentation.

## Remove connections

If [LoadBalanceTimeout](/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder.loadbalancetimeout) (or `Connection Lifetime`) is set, when a connection is returned to the pool, its creation time is compared with the current time and the connection is destroyed if that time span (in seconds) exceeds the value specified by `LoadBalanceTimeout`. This is useful in clustered configurations to force load balancing between a running server and a server just brought online.

If LoadBalanceTimeout (or Connection Lifetime) isn't set (default value = 0), the connection pooler removes a connection from the pool after it has been idle for approximately **4-8** minutes (in a random two-pass fashion), or if the pooler detects that the connection with the server has been severed.

> [!NOTE]
> A severed connection can be detected only after attempting to communicate with the server. If a connection is found that is no longer connected to the server, it is marked as invalid. Invalid connections are removed from the connection pool only when they are closed or reclaimed.

If a connection exists to a server that has disappeared, this connection can be drawn from the pool even if the connection pooler has not detected the severed connection and marked it as invalid. This is the case because the overhead of checking that the connection is still valid would eliminate the benefits of having a pooler by causing another round trip to the server to occur. When this occurs, the first attempt to use the connection will detect that the connection has been severed, and an exception is thrown.

## Clear the pool

Microsoft SqlClient Data Provider for SQL Server introduced two new methods to clear the pool: <xref:Microsoft.Data.SqlClient.SqlConnection.ClearAllPools%2A> and <xref:Microsoft.Data.SqlClient.SqlConnection.ClearPool%2A>. `ClearAllPools` clears the connection pools for a given provider, and `ClearPool` clears the connection pool that is associated with a specific connection.

> [!NOTE]
> If there are connections being used at the time of the call, they are marked appropriately. When they are closed, they are discarded instead of being returned to the pool.

## Transaction support

Connections are drawn from the pool and assigned based on transaction context. Unless `Enlist=false` is specified in the connection string, the connection pool makes sure that the connection is enlisted in the <xref:System.Transactions.Transaction.Current%2A> context. When a connection is closed and returned to the pool with an enlisted `System.Transactions` transaction, it is set aside in such a way that the next request for that connection pool with the same `System.Transactions` transaction will return the same connection if it is available. If such a request is issued, and there are no pooled connections available, a connection is drawn from the non-transacted part of the pool and enlisted. If no connections are available in either area of the pool, a new connection is created and enlisted.

When a connection is closed, it is released back into the pool and into the appropriate subdivision based on its transaction context. Therefore, you can close the connection without generating an error, even though a distributed transaction is still pending. This allows you to commit or abort the distributed transaction later.

## Control connection pooling with connection string keywords

The `ConnectionString` property of the <xref:Microsoft.Data.SqlClient.SqlConnection> object supports connection string key/value pairs that can be used to adjust the behavior of the connection pooling logic. For more information, see <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.

## Pool fragmentation

Pool fragmentation is a common problem in many Web applications where the application can create a large number of pools that are not freed until the process exits. This leaves a large number of connections open and consuming memory, which results in poor performance.

### Pool fragmentation due to integrated security

Connections are pooled according to the connection string plus the user identity. Therefore, if you use Basic authentication or Windows Authentication on the Web site and an integrated security login, you get one pool per user. Although this improves the performance of subsequent database requests for a single user, that user cannot take advantage of connections made by other users. It also results in at least one connection per user to the database server. This is a side effect of a particular Web application architecture that developers must weigh against security and auditing requirements.

### Pool fragmentation due to many databases

Many Internet service providers host several Web sites on a single server. They may use a single database to confirm a Forms authentication login and then open a connection to a specific database for that user or group of users. The connection to the authentication database is pooled and used by everyone. However, there is a separate pool of connections to each database, which increase the number of connections to the server.

This is also a side-effect of the application design. There is a relatively simple way to avoid this side effect without compromising security when you connect to SQL Server. Instead of connecting to a separate database for each user or group, connect to the same database on the server and then execute the Transact-SQL USE statement to change to the desired database.
 
The following code fragment demonstrates creating an initial connection to the `master` database and then switching to the desired database specified in the `databaseName` string variable.

[!code-csharp[SqlConnection_Pooling_Use_Statement#1](~/../sqlclient/doc/samples/SqlConnection_Pooling_Use_Statement.cs#1)]

## Application roles and connection pooling

After a SQL Server application role has been activated by calling the `sp_setapprole` system stored procedure, the security context of that connection cannot be reset. However, if pooling is enabled, the connection is returned to the pool, and an error occurs when the pooled connection is reused.

### Application role alternatives

We recommend that you take advantage of security mechanisms that you can use instead of application roles.

## See also

- [Connection pooling](connection-pooling.md)
- [SQL Server and ADO.NET](./sql/index.md)
- [Diagnostic counters in SqlClient](diagnostic-counters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
