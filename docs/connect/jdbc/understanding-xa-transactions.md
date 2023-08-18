---
title: Understanding XA transactions
description: The Microsoft JDBC Driver for SQL Server provides support for Java Platform, Enterprise Edition/JDBC 2.0 optional distributed transactions.
author: David-Engel
ms.author: v-davidengel
ms.date: 04/17/2023
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
---
# Understanding XA transactions

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

The [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] provides support for Java Platform, Enterprise Edition/JDBC 2.0 optional distributed transactions. JDBC connections obtained from the [SQLServerXADataSource](reference/sqlserverxadatasource-class.md) class can participate in standard distributed transaction processing environments such as Java Platform, Enterprise Edition (Java EE) application servers.

In this article, XA stands for extended architecture.

> [!WARNING]
> Microsoft JDBC Driver 4.2 (and higher) for SQL includes new timeout options for the existing feature for automatic rollback of unprepared transactions. See [Configuring server-side timeout settings for automatic rollback of unprepared transactions](understanding-xa-transactions.md#BKMK_ServerSide) later in this topic for more detail.

## Remarks

The classes for the distributed transaction implementation are as follows:

| Class                                              | Implements                      | Description                                       |
| -------------------------------------------------- | ------------------------------- | ------------------------------------------------- |
| com.microsoft.sqlserver.jdbc.SQLServerXADataSource | javax.sql.XADataSource          | The class factory for distributed connections.    |
| com.microsoft.sqlserver.jdbc.SQLServerXAResource   | javax.transaction.xa.XAResource | The resource adapter for the transaction manager. |

> [!NOTE]
> XA distributed transaction connections default to the Read Committed isolation level.

## Guidelines and limitations when using XA transactions

The following extra guidelines apply to tightly coupled transactions:

- When you use XA transactions together with Microsoft Distributed Transaction Coordinator (MS DTC), you may notice that the current version of MS DTC doesn't support tightly coupled XA branch behavior. For example, MS DTC has a one-to-one mapping between an XA branch transaction ID (XID) and an MS DTC transaction ID and work that loosely coupled XA branches perform is isolated from one another.

- MS DTC also supports tightly coupled XA branches where multiple XA branches with same global transaction ID (GTRID) are mapped to a single MS DTC transaction ID. This support enables multiple tightly coupled XA branches to see each other's changes in the resource manager, such as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

- A [SSTRANSTIGHTLYCPLD](reference/sstranstightlycpld-field-sqlserverxaresource.md) flag allows applications to use tightly coupled XA transactions, which have different XA branch transaction IDs (BQUAL) but have the same global transaction ID (GTRID) and format ID (FormatID). In order to use that feature, you must set the [SSTRANSTIGHTLYCPLD](reference/sstranstightlycpld-field-sqlserverxaresource.md) on the flags parameter of the XAResource.start method:

    ```java
    xaRes.start(xid, SQLServerXAResource.SSTRANSTIGHTLYCPLD);
    ```

## Configuration instructions

The following steps are required if you want to use XA data sources together with Microsoft Distributed Transaction Coordinator (MS DTC) for handling distributed transactions. The high-level steps are:

1. Ensure the MS DTC service is running and starts automatically.
1. Configure server-side components.
1. Configure server-side timeout (optional).
1. Grant access to users.

### Running the MS DTC service

The MS DTC service should be marked **Automatic** in Service Manager to make sure that it's running when the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service is started. To enable MS DTC for XA transactions, you must follow these steps:

On Windows Vista and later:

1. Select the **Start** button, type **dcomcnfg** in the Start **Search** box, and then press ENTER to open **Component Services**. You can also type `%windir%\system32\comexp.msc` in the **StartSearch** box to open **Component Services**.

2. Expand Component Services, Computers, My Computer, and then Distributed Transaction Coordinator.

3. Right-click **Local DTC** and then select **Properties**.

4. Select the **Security** tab on the **Local DTC Properties** dialog box.

5. Select the **Enable XA Transactions** check box, and then select **OK**. This action causes an MS DTC service restart.

6. Select **OK** again to close the **Properties** dialog box, and then close **Component Services**.

7. Stop and then restart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to make sure that it syncs with the MS DTC changes. (This step is optional for SQL Server 2019 and SQL Server 2017 CU 16 and higher.)

### Configuring the JDBC distributed transaction components

The steps for configuring server-side components differ depending on your target server version. To check your server version, execute the query `SELECT @@VERSION` against the server and view the output. For SQL Server 2017 Cumulative Update (CU) 16 and higher, follow the [SQL Server 2017 CU16 and higher](#sql-server-2017-cu16-and-higher) instructions. For older SQL Server versions, follow the [SQL Server 2017 CU15 and lower](#sql-server-2017-cu15-and-lower) instructions.

#### SQL Server 2017 CU16 and higher

To enable the required components to perform XA distributed transactions using the JDBC driver, execute the following stored procedure.

```sql
EXEC sp_sqljdbc_xa_install
```

To disable the components, execute the following stored procedure.

```sql
EXEC sp_sqljdbc_xa_uninstall
```

Skip to the [Configuring server-side timeout settings for automatic rollback of unprepared transactions](#BKMK_ServerSide) section.

#### SQL Server 2017 CU15 and lower

> [!NOTE]
> The JDBC distributed transaction components are included in the xa directory of the JDBC driver installation. These components include the xa_install.sql and sqljdbc_xa.dll files. If you have different versions of the JDBC driver on different clients, it is recommended to use the newest sqljdbc_xa.dll on the server.

You can configure the JDBC driver distributed transaction components by following these steps:

1. Copy the new sqljdbc_xa.dll from the JDBC driver installation directory to the Binn directory of every [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer that participates in distributed transactions.

    > [!NOTE]
    > If you are using XA transactions with a 32-bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (only applicable to SQL Server 2014 or older), use the sqljdbc_xa.dll file in the x86 folder, even if the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is installed on a x64 processor. If you are using XA transactions with a 64-bit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] on the x64 processor, use the sqljdbc_xa.dll file in the x64 folder.

2. Execute the database script xa_install.sql on every [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance that participates in distributed transactions. This script installs the extended stored procedures that are called by sqljdbc_xa.dll. These extended stored procedures implement distributed transaction and XA support for the [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]. You need to run this script as an administrator of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.

3. To grant permissions to a specific user to participate in distributed transactions with the JDBC driver, add the user to the SqlJDBCXAUser role.

You can configure only one version of the sqljdbc_xa.dll assembly on each [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance at a time. Applications may need to use different versions of the JDBC driver to connect to the same [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance by using the XA connection. In that case, sqljdbc_xa.dll, which comes with the newest JDBC driver, must be installed on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.

There are three ways to verify the version of sqljdbc_xa.dll currently installed on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance:

1. Open the LOG directory of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer that participates in distributed transactions. Select and open the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "ERRORLOG" file. Search for "Using 'SQLJDBC_XA.dll' version ..." phrase in the "ERRORLOG" file.

2. Open the Binn directory of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer that participates in distributed transactions. Select the sqljdbc_xa.dll assembly.

    - On Windows Vista or later: Right-click sqljdbc_xa.dll and then select Properties. Then select the **Details** tab. The **File Version** field shows the version of sqljdbc_xa.dll that is currently installed on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance.

3. Set the logging functionality as shown in the code example in the next section. Search for "Server XA DLL version:..." phrase in the output log file.

#### Upgrading sqljdbc_xa.dll

When you install a new version of the JDBC driver, you should also use sqljdbc_xa.dll from the new version to upgrade sqljdbc_xa.dll on the server.

> [!IMPORTANT]
> You should upgrade sqljdbc_xa.dll during a maintenance window or when there are no MS DTC transactions in progress.

1. Unload sqljdbc_xa.dll using the [!INCLUDE[tsql](../../includes/tsql-md.md)] command:

    ```sql
    DBCC sqljdbc_xa (FREE)
    ```

2. Copy the new sqljdbc_xa.dll from the JDBC driver installation directory to the Binn directory of every [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computer that participates in distributed transactions.

    The new DLL is loaded when an extended procedure in sqljdbc_xa.dll is called. You don't need to restart [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] to load the new definitions.

### <a name="BKMK_ServerSide"></a> Configuring server-side timeout settings for automatic rollback of unprepared transactions

There are two registry settings (DWORD values) to control the timeout behavior of distributed transactions:

- `XADefaultTimeout` (in seconds): The default timeout value to be used when the user doesn't specify any timeout. The default is 0.

- `XAMaxTimeout` (in seconds): The maximum value of the timeout that a user can set. The default is 0.

These settings are SQL Server instance specific and should be created under the following registry key:

```bash
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout
```

> [!NOTE]
> For 32-bit SQL Server running in 64-bit machines (only applicable to SQL Server 2014 and older), the registry settings should be created under the following key: `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Microsoft SQL Server\MSSQL<version>.<instance_name>\XATimeout`

A timeout value is set for each transaction when it's started and SQL Server rolls back the transaction if the timeout expires. The timeout is determined depending on these registry settings and depending on what the user has specified through XAResource.setTransactionTimeout(). A few examples on how these timeout values are interpreted as follows:

- `XADefaultTimeout = 0`, `XAMaxTimeout = 0`

     Means no default timeout is used, and no maximum timeout is enforced on clients. In this case, the transactions have a timeout only if the client sets a timeout using XAResource.setTransactionTimeout.

- `XADefaultTimeout = 60`, `XAMaxTimeout = 0`

     Means all transactions have a 60-second timeout if the client doesn't specify any timeout. If the client specifies a timeout, then that timeout value is used. No maximum value for timeout is enforced.

- `XADefaultTimeout = 30`, `XAMaxTimeout = 60`

     Means all transactions have a 30-second timeout if the client doesn't specify any timeout. If client specifies any timeout, then the client's timeout is used as long as it's less than 60 seconds (the max value).

- `XADefaultTimeout = 0`, `XAMaxTimeout = 30`

     Means all transactions have a 30-second timeout (the max value) if the client doesn't specify any timeout. If the client specifies any timeout, then the client's timeout is used as long as it's less than 30 seconds (the max value).

### Configuring the user-defined roles

To grant permissions to a specific user to participate in distributed transactions with the JDBC driver, add the user to the SqlJDBCXAUser role. For example, use the following [!INCLUDE[tsql](../../includes/tsql-md.md)] code to add a user named 'shelly' (SQL standard login user named 'shelly') to the SqlJDBCXAUser role:

```sql
USE master
GO
EXEC sp_grantdbaccess 'shelly', 'shelly'
GO
EXEC sp_addrolemember [SqlJDBCXAUser], 'shelly'
```

SQL user-defined roles are defined per database. To create your own role for security purposes, you have to define the role in each database, and add users in a per database manner. The SqlJDBCXAUser role is strictly defined in the master database because it's used to grant access to the SQL JDBC extended stored procedures that reside in master. You have to first grant individual users access to master, and then grant them access to the SqlJDBCXAUser role while you're logged into the master database.

## Example

```java
import java.net.Inet4Address;
import java.sql.*;
import java.util.Random;
import javax.sql.XAConnection;
import javax.transaction.xa.*;
import com.microsoft.sqlserver.jdbc.*;


public class testXA {

    public static void main(String[] args) throws Exception {

        // Create variables for the connection string.
        String prefix = "jdbc:sqlserver://";
        String serverName = "localhost";
        int portNumber = 1433;
        String databaseName = "AdventureWorks";
        String user = "UserName";
        String password = "*****";

        String connectionUrl = prefix + serverName + ":" + portNumber + ";encrypt=true;databaseName=" + databaseName + ";user="
                + user + ";password=" + password;

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            stmt.executeUpdate("CREATE TABLE XAMin (f1 int, f2 varchar(max))");

        }
        // Create the XA data source and XA ready connection.
        SQLServerXADataSource ds = new SQLServerXADataSource();
        ds.setUser(user);
        ds.setPassword(password);
        ds.setServerName(serverName);
        ds.setPortNumber(portNumber);
        ds.setDatabaseName(databaseName);

        XAConnection xaCon = ds.getXAConnection();
        try (Connection con = xaCon.getConnection()) {

            // Get a unique Xid object for testing.
            XAResource xaRes = null;
            Xid xid = null;
            xid = XidImpl.getUniqueXid(1);

            // Get the XAResource object and set the timeout value.
            xaRes = xaCon.getXAResource();
            xaRes.setTransactionTimeout(0);

            // Perform the XA transaction.
            System.out.println("Write -> xid = " + xid.toString());
            xaRes.start(xid, XAResource.TMNOFLAGS);
            PreparedStatement pstmt = con.prepareStatement("INSERT INTO XAMin (f1,f2) VALUES (?, ?)");
            pstmt.setInt(1, 1);
            pstmt.setString(2, xid.toString());
            pstmt.executeUpdate();

            // Commit the transaction.
            xaRes.end(xid, XAResource.TMSUCCESS);
            xaRes.commit(xid, true);
        }
        xaCon.close();

        // Open a new connection and read back the record to verify that it worked.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT * FROM XAMin")) {
            rs.next();
            System.out.println("Read -> xid = " + rs.getString(2));
            stmt.executeUpdate("DROP TABLE XAMin");
        }
    }
}


class XidImpl implements Xid {

    public int formatId;
    public byte[] gtrid;
    public byte[] bqual;

    public byte[] getGlobalTransactionId() {
        return gtrid;
    }

    public byte[] getBranchQualifier() {
        return bqual;
    }

    public int getFormatId() {
        return formatId;
    }

    XidImpl(int formatId, byte[] gtrid, byte[] bqual) {
        this.formatId = formatId;
        this.gtrid = gtrid;
        this.bqual = bqual;
    }

    public String toString() {
        int hexVal;
        StringBuffer sb = new StringBuffer(512);
        sb.append("formatId=" + formatId);
        sb.append(" gtrid(" + gtrid.length + ")={0x");
        for (int i = 0; i < gtrid.length; i++) {
            hexVal = gtrid[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(gtrid[i] & 0xFF));
            else
                sb.append(Integer.toHexString(gtrid[i] & 0xFF));
        }
        sb.append("} bqual(" + bqual.length + ")={0x");
        for (int i = 0; i < bqual.length; i++) {
            hexVal = bqual[i] & 0xFF;
            if (hexVal < 0x10)
                sb.append("0" + Integer.toHexString(bqual[i] & 0xFF));
            else
                sb.append(Integer.toHexString(bqual[i] & 0xFF));
        }
        sb.append("}");
        return sb.toString();
    }

    // Returns a globally unique transaction id.
    static byte[] localIP = null;
    static int txnUniqueID = 0;

    static Xid getUniqueXid(int tid) {

        Random rnd = new Random(System.currentTimeMillis());
        txnUniqueID++;
        int txnUID = txnUniqueID;
        int tidID = tid;
        int randID = rnd.nextInt();
        byte[] gtrid = new byte[64];
        byte[] bqual = new byte[64];
        if (null == localIP) {
            try {
                localIP = Inet4Address.getLocalHost().getAddress();
            } catch (Exception ex) {
                localIP = new byte[] {0x01, 0x02, 0x03, 0x04};
            }
        }
        System.arraycopy(localIP, 0, gtrid, 0, 4);
        System.arraycopy(localIP, 0, bqual, 0, 4);

        // Bytes 4 -> 7 - unique transaction id.
        // Bytes 8 ->11 - thread id.
        // Bytes 12->15 - random number generated by using seed from current time in milliseconds.
        for (int i = 0; i <= 3; i++) {
            gtrid[i + 4] = (byte) (txnUID % 0x100);
            bqual[i + 4] = (byte) (txnUID % 0x100);
            txnUID >>= 8;
            gtrid[i + 8] = (byte) (tidID % 0x100);
            bqual[i + 8] = (byte) (tidID % 0x100);
            tidID >>= 8;
            gtrid[i + 12] = (byte) (randID % 0x100);
            bqual[i + 12] = (byte) (randID % 0x100);
            randID >>= 8;
        }
        return new XidImpl(0x1234, gtrid, bqual);
    }
}
```

## See also

[Performing transactions with the JDBC driver](performing-transactions-with-the-jdbc-driver.md)
