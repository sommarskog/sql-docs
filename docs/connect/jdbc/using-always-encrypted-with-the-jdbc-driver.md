---
title: Use Always Encrypted with the JDBC driver
description: Learn how to use Always Encrypted with the JDBC driver to encrypt sensitive data on the server.
author: David-Engel
ms.author: v-davidengel
ms.date: 08/08/2022
ms.service: sql
ms.subservice: connectivity
ms.topic: conceptual
---

# Use Always Encrypted with the JDBC driver

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

This page provides information on how to develop Java applications to use [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) with the Microsoft JDBC Driver 6.0 (or higher) for SQL Server.

Always Encrypted allows clients to encrypt sensitive data and never reveal the data or the encryption keys to SQL Server or Azure SQL Database. An Always Encrypted enabled driver, such as the Microsoft JDBC Driver 6.0 (or higher) for SQL Server, achieves this behavior by transparently encrypting and decrypting sensitive data in the client application. The driver figures out which query parameters correspond to Always Encrypted database columns, and encrypts the values of those parameters before it sends them to the database. Similarly, the driver transparently decrypts data retrieved from encrypted database columns in query results. For more information, see [Always Encrypted (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) and [Always Encrypted API reference for the JDBC driver](always-encrypted-api-reference-for-the-jdbc-driver.md).

## Prerequisites

- Make sure Microsoft JDBC Driver 6.0 (or higher) for SQL Server is installed on your development machine.
- Download and install the Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files.  Be sure to read the Readme included in the zip file for installation instructions, and relevant details on possible export or import issues.
  - For mssql-jdbc-X.X.X.jre7.jar or sqljdbc41.jar, the policy files can be downloaded from [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
  - For mssql-jdbc-X.X.X.jre8.jar or sqljdbc42.jar, the policy files can be downloaded from  [Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 8 Download](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)
  - For mssql-jdbc-X.X.X.jre9.jar, no policy file needs to be downloaded. The jurisdiction policy in Java 9 defaults to unlimited strength encryption.

## Work with column master key stores

To encrypt or decrypt data for encrypted columns, SQL Server maintains column encryption keys. Column encryption keys are stored in encrypted form in the database metadata. Each column encryption key has a corresponding column master key that is used to encrypt the column encryption key.

The database metadata doesn't contain the column master keys. Those keys are only held by the client. However the database metadata does contain information about where the column master keys are stored relative to the client. For example, the database metadata might say the keystore that holds a column master key is the Windows Certificate Store, and the specific certificate that's used to encrypt and decrypt is located at a specific path within the Windows Certificate Store.

If the client has access to that certificate in the Windows Certificate Store, it can obtain the certificate. The certificate can then be used to decrypt the column encryption key. Then that encryption key can be used to decrypt or encrypt data for encrypted columns that use that column encryption key.

The Microsoft JDBC Driver for SQL Server communicates with a keystore that uses a column master key store provider, which is an instance of a class that's derived from **`SQLServerColumnEncryptionKeyStoreProvider`**.

### Use built-in column master key store providers

The Microsoft JDBC Driver for SQL Server comes with the following built-in column master key store providers. Some of these providers are pre-registered with the specific provider names (used to look up the provider) and some require either extra credentials or explicit registration.

| Class                                                 | Description                                        | Provider (lookup) name  | Is pre-registered? | Platform |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- | :------- |
| **`SQLServerColumnEncryptionAzureKeyVaultProvider`**    | A provider for a keystore for the Azure Key Vault. | AZURE_KEY_VAULT         | _No_ before JDBC driver version 7.4.1, but _yes_ as of JDBC driver version 7.4.1. | Windows, Linux, macOS |
| **`SQLServerColumnEncryptionCertificateStoreProvider`** | A provider for the Windows Certificate Store.      | MSSQL_CERTIFICATE_STORE | _Yes_                | Windows |
| **`SQLServerColumnEncryptionJavaKeyStoreProvider`**     | A provider for the Java keystore.                  | MSSQL_JAVA_KEYSTORE     | _Yes_                | Windows, Linux, macOS |

For the pre-registered keystore providers, you don't need any application code changes to use these providers but note the following items:

- You must make sure the provider name that's configured in the column master key metadata is correct and the column master key path follows the key path format that is valid for a given provider. It's recommended that you configure the keys with tools such as SQL Server Management Studio, which automatically generates the valid provider names and key paths to issue the `CREATE COLUMN MASTER KEY` (Transact-SQL) statement.
- Ensure your application can access the key in the keystore. This task might involve granting your application access to the key and/or the keystore. Depending on the keystore, this might involve other keystore-specific configuration steps. For example, to use the `SQLServerColumnEncryptionJavaKeyStoreProvider`, you must provide the location and the password of the keystore in the connection properties.

All of these keystore providers are described in more detail in the sections that follow. You only need to implement one keystore provider to use Always Encrypted.

### Use Azure Key Vault provider

Azure Key Vault is a convenient option to store and manage column master keys for Always Encrypted (especially if your application is hosted in Azure). The Microsoft JDBC Driver for SQL Server includes a built-in provider, `SQLServerColumnEncryptionAzureKeyVaultProvider`, for applications that have keys stored in Azure Key Vault. The name of this provider is AZURE_KEY_VAULT.

> [!NOTE]
> The Azure Key Vault provider built in to the JDBC driver supports both [Vaults and Managed HSMs in Azure Key Vault](/azure/key-vault/keys/about-keys).

To use the Azure Key Vault store provider, an application developer must create the vault and the keys in Azure Key Vault and create an App registration in Azure Active Directory. The registered application must be granted Get, Decrypt, Encrypt, Unwrap Key, Wrap Key, and Verify permissions in the Access policies defined for the key vault created for use with Always Encrypted. For more information on how to set up the key vault and create a column master key, see [Azure Key Vault—Step by Step](/archive/blogs/kv/azure-key-vault-step-by-step) and [Creating Column Master Keys in Azure Key Vault](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault).

For Azure Key Vault provider, the JDBC driver validates the column master key path against the list of trusted endpoints. As of version 8.2.2, this list is configurable: create a `mssql-jdbc.properties` file in the working directory of the application, set the `AKVTrustedEndpoints` property to a semicolon-delimited list. If the value begins with a semicolon, it extends the default list. Otherwise, it replaces the default list.

The default, trusted endpoints are:

- **`*vault.azure.net`**
- **`*vault.azure.cn`**
- **`*vault.usgovcloudapi.net`**
- **`*vault.microsoftazure.de`**
- **`*managedhsm.azure.net`** (v9.2+)
- **`*managedhsm.azure.cn`** (v9.2+)
- **`*managedhsm.usgovcloudapi.net`** (v9.2+)
- **`*managedhsm.microsoftazure.de`** (v9.2+)

For the examples on this page, if you've created an Azure Key Vault based column master key and column encryption key with SQL Server Management Studio, the T-SQL script to re-create them might look similar to this example with its own specific **KEY_PATH** and **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyVaultName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
);
```

An application that uses the JDBC driver can use the Azure Key Vault. The syntax or statements for this use of Azure Key Vault changed as of with JDBC driver version 7.4.1.

#### JDBC driver 7.4.1 or later

This section involves JDBC driver version 7.4.1 or later.

A client application that uses the JDBC driver can configure to use Azure Key Vault by mentioning `keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>` in JDBC connection string.

Here's an example that provides this configuration information in a JDBC connection string.

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>";
```

The JDBC driver automatically instantiates a **`SQLServerColumnEncryptionAzureKeyVaultProvider`** object when these credentials are present among the connection properties.

> [!IMPORTANT]
> The connection properties **`keyVaultProviderClientId`** and **`keyVaultProviderClientKey`** have been deprecated as of v8.4.1. Users are encouraged to use **`keyStoreAuthentication`**, **`KeyStorePrincipalId`**, and **`KeyStoreSecret`** instead.

#### JDBC driver versions before 7.4.1

This section involves JDBC driver versions before 7.4.1.

A client application that uses the JDBC driver must instantiate a **`SQLServerColumnEncryptionAzureKeyVaultProvider`** object, and then register the object with the driver.

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**`clientID`** is the Application ID of an App registration in an Azure Active Directory instance. **`clientKey`** is a Key Password registered under that Application, which provides API access to the Azure Key Vault.

After the application creates an instance of `SQLServerColumnEncryptionAzureKeyVaultProvider`, the application must register the instance with the driver with the `SQLServerConnection.registerColumnEncryptionKeyStoreProviders()` method. It's highly recommended that the instance is registered using the default lookup name, AZURE_KEY_VAULT, which can be obtained by the `SQLServerColumnEncryptionAzureKeyVaultProvider.getName()` API. The default name allows you to use tools such as SQL Server Management Studio or PowerShell to provision and manage Always Encrypted keys (the tools use the default name to generate the metadata object to column master key). The following example shows registering the Azure Key Vault provider. For more information on the `SQLServerConnection.registerColumnEncryptionKeyStoreProviders()` method, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md).

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
> If you use the Azure Key Vault keystore provider, the Azure Key Vault implementation of the JDBC driver has dependencies on these libraries (from GitHub) which must be included with your application:
>
> [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
> [microsoft-authentication-library-for-java libraries](https://github.com/AzureAD/microsoft-authentication-library-for-java)
>
> For an example of how to include these dependencies in a Maven project, see [Download MSAL4J And AKV Dependencies with Apache Maven](https://github.com/microsoft/mssql-jdbc/wiki/Download-MSAL4J-And-AKV-Dependencies-with-Apache-Maven)

### Use Azure Key Vault authentication with Managed Identities

As of JDBC Driver **8.4.1**, the driver added support to authenticate to Azure Key Vaults with Managed Identities.

You can use [Managed Identities](/azure/active-directory/managed-identities-azure-resources/overview) to authenticate to the Azure Key Vault if the application is hosted in Azure. This eliminates the need to provide and expose any credentials in the code.

#### Connection properties for Key Vault authentication with Managed Identities

For JDBC Driver 8.4.1 and later, the driver introduced the following connection properties:

| ConnectionProperty    | Possible Value Pairing 1 | Possible Value Pairing 2 | Possible Value Pairing 3 |
| ---|---|---|----|
| keyStoreAuthentication| KeyVaultClientSecret   |KeyVaultManagedIdentity |JavaKeyStorePassword |
| keyStorePrincipalId   | \<Azure AD Application Client ID\>    | \<Azure AD Application object ID\> (optional)| n/a |
| keyStoreSecret        | \<Azure AD Application Client Secret\>|n/a|\<secret/password for the Java Key Store\> |

The following examples show how the connection properties are used in a connection string.

#### Use Managed Identity to authenticate to AKV

```java
"jdbc:sqlserver://<server>:<port>;encrypt=true;columnEncryptionSetting=Enabled;keyStoreAuthentication=KeyVaultManagedIdentity;"
```

#### Use Managed Identity and the principal ID to authenticate to AKV

```java
"jdbc:sqlserver://<server>:<port>;encrypt=true;columnEncryptionSetting=Enabled;keyStoreAuthentication=KeyVaultManagedIdentity;keyStorePrincipal=<principalId>"
```

#### Use clientId and clientSecret to authentication to AKV

```java
"jdbc:sqlserver://<server>:<port>;encrypt=true;columnEncryptionSetting=Enabled;keyStoreAuthentication=KeyVaultClientSecret;keyStorePrincipalId=<clientId>;keyStoreSecret=<clientSecret>"
```

Users are encouraged to use these connection properties to specify the type of authentication used for the Key Stores instead of the `SQLServerColumnEncryptionAzureKeyVaultProvider` API.

Previously added connection properties `keyVaultProviderClientId` and `keyVaultProviderClientKey` are deprecated and replaced by the connection properties described above.

For information on how to configure Managed Identities, see [Configure managed identities for Azure resources on a VM using the Azure portal](/azure/active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm).

### Use Windows Certificate Store provider

The `SQLServerColumnEncryptionCertificateStoreProvider` can be used to store column master keys in the Windows Certificate Store. Use the SQL Server Management Studio (SSMS) Always Encrypted wizard or other supported tools to create the column master key and column encryption key definitions in the database. The same wizard can be used to generate a self-signed certificate in the Windows Certificate Store that can be used as a column master key for the Always Encrypted data. For more information on column master key and column encryption key T-SQL syntax, see [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) and [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) respectively.

The name of the `SQLServerColumnEncryptionCertificateStoreProvider` is MSSQL_CERTIFICATE_STORE and can be queried by the getName() API of the provider object. It's automatically registered by the driver and can be used seamlessly without any application change.

For the examples on this page, if you've created a Windows Certificate Store based column master key and column encryption key with SQL Server Management Studio, the T-SQL script to re-create them might look similar to this example with its own specific **KEY_PATH** and **ENCRYPTED_VALUE**:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
);
```

> [!IMPORTANT]
> While the other keystore providers in this article are available on all platforms supported by the driver, the `SQLServerColumnEncryptionCertificateStoreProvider` implementation of the JDBC driver is available on Windows operating systems only. It has a dependency on the `mssql-jdbc_auth-<version>-<arch>.dll` that is available in the driver package. To use this provider, copy the `mssql-jdbc_auth-<version>-<arch>.dll` file to a directory on the Windows system path on the computer where the JDBC driver is installed. Alternatively you can set the java.library.path system property to specify the directory of the `mssql-jdbc_auth-<version>-<arch>.dll`. If you are running a 32-bit Java Virtual Machine (JVM), use the `mssql-jdbc_auth-<version>-x86.dll` file in the x86 folder, even if the operating system is the x64 version. If you are running a 64-bit JVM on a x64 processor, use the `mssql-jdbc_auth-<version>-x64.dll` file in the x64 folder. For example, if you use the 32-bit JVM and the JDBC driver is installed in the default directory, you can specify the location of the DLL with the following virtual machine (VM) argument when the Java application is started:
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### Use Java Key Store provider

The JDBC driver comes with a built-in keystore provider implementation for the Java Key Store. If the **`keyStoreAuthentication`** connection string property is present in the connection string and it's set to `JavaKeyStorePassword`, the driver automatically instantiates and registers the provider for Java Key Store. The name of the Java Key Store provider is MSSQL_JAVA_KEYSTORE. This name can also be queried by the `SQLServerColumnEncryptionJavaKeyStoreProvider.getName()` API.

There are three connection string properties that allow a client application to specify the credentials the driver needs to authenticate to the Java Key Store. The driver initializes the provider based on the values of these three properties in the connection string.

**`keyStoreAuthentication`:** Identifies the Java Key Store to use. With Microsoft JDBC Driver 6.0 and higher for SQL Server, you can authenticate to the Java Key Store only through this property. For the Java Key Store, the value for this property must be `JavaKeyStorePassword`.

**`keyStoreLocation`:** The path to the Java Key Store file that stores the column master key. The path includes the keystore filename.

**`keyStoreSecret`:** The secret/password to use for the keystore and the key. To use the Java Key Store, the keystore and the key password must be the same.

Here's an example of providing these credentials in the connection string:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

You can also get or set these settings with the `SQLServerDataSource` object. For more information, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md).

The JDBC driver automatically instantiates the `SQLServerColumnEncryptionJavaKeyStoreProvider` when these credentials are present in connection properties.

### Creating a column master key for the Java Key Store

The `SQLServerColumnEncryptionJavaKeyStoreProvider` can be used with JKS or PKCS12 keystore types. To create or import a key to use with this provider use the Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) utility. The key must have the same password as the keystore itself. Here's an example of how to create a public key and its associated private key with the `keytool` utility:

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

This command creates a public key and wraps it in an X.509 self-signed certificate, which is stored in the keystore `keystore.jks` along with its associated private key. This entry in the keystore is identified by the alias `AlwaysEncryptedKey`.

Here's an example of the same with a PKCS12 store type:

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

If the keystore is of type PKCS12, the keytool utility doesn't prompt for a key password and the key password needs to be provided with `-keypass` option as the **`SQLServerColumnEncryptionJavaKeyStoreProvider`** requires that the keystore and the key have the same password.

You can also export a certificate from the Windows Certificate store in .pfx format and use that with the **`SQLServerColumnEncryptionJavaKeyStoreProvider`**. The exported certificate can also be imported to the Java Key Store as a JKS keystore type.

After you create the keytool entry, create the column master key metadata in the database, which needs the keystore provider name and the key path. For more information on how to create column master key meta data, see [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md). For `SQLServerColumnEncryptionJavaKeyStoreProvider`, the key path is just the alias of the key and the name of the `SQLServerColumnEncryptionJavaKeyStoreProvider` is `MSSQL_JAVA_KEYSTORE`. You can also query this name with the `getName()` public API of the `SQLServerColumnEncryptionJavaKeyStoreProvider` class.

The T-SQL syntax to create the column master key is:

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
);
```

For the 'AlwaysEncryptedKey' created above, the column master key definition would be:

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
);
```

> [!NOTE]
> The built-in SQL Server management Studio functionality cannot create column master key definitions for the Java Key Store. T-SQL commands must be used programmatically.

### Create a column encryption key for the Java Key Store

The SQL Server Management Studio or any other tool can't be used to create column encryption keys using column master keys in the Java Key Store. The client application must create the column encryption key programmatically with the `SQLServerColumnEncryptionJavaKeyStoreProvider` class. For more information, see [Use column master key store providers for programmatic key provisioning](#use-column-master-key-store-providers-for-programmatic-key-provisioning).

### Implementing a custom column master key store provider

If you want to store column master keys in a keystore that isn't supported by an existing provider, you can implement a custom provider by extending the `SQLServerColumnEncryptionKeyStoreProvider` Class and registering the provider with one of the following methods:

- `SQLServerConnection.registerColumnEncryptionKeyStoreProviders`
- `SQLServerConnection.registerColumnEncryptionKeyStoreProvidersOnConnection` (Added in JDBC version 10.2)
- `SQLServerStatement.registerColumnEncryptionKeyStoreProvidersOnStatement` (Added in JDBC version 10.2)

```java
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

Register the provider with `SQLServerConnection.registerColumnEncryptionKeyStoreProviders`:

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

#### Column encryption key cache precedence

This section applies to JDBC driver version 10.2 and higher.

The column encryption keys (CEK) decrypted by custom key store providers registered on a connection or statement instance won't be cached by the **Microsoft JDBC Driver for SQL Server**. Custom key store providers should implement their own CEK caching mechanism.

As of version 10.2, the `SQLServerColumnEncryptionAzureKeyVaultProvider` has its own CEK caching implementation. When registered on a connection or statement instance, CEKs decrypted by an instance of `SQLServerColumnEncryptionAzureKeyVaultProvider` will be cleared when that instance goes out of scope:

```java
try (SQLServerConnection conn = getConnection(); SQLServerStatement stmt = (SQLServerStatement) conn.createStatement()) {

    Map<String, SQLServerColumnEncryptionKeyStoreProvider> customKeyStoreProviders = new HashMap<>();
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    customKeyStoreProviders.put(akvProvider.getName(), akvProvider);
    stmt.registerColumnEncryptionKeyStoreProvidersOnStatement(customKeyStoreProviders);
    // Perform database operation with Azure Key Vault Provider
    // Any decrypted column encryption keys will be cached              
} // Column encryption key cache of "akvProvider" is cleared when "akvProvider" goes out of scope
```

> [!NOTE]
> CEK caching implemented by custom key store providers will be disabled by the driver if the key store provider instance is registered in the driver globally with the `SQLServerConnection.registerColumnEncryptionKeyStoreProviders` method. Any CEK caching implementation should reference the value of time-to-live duration before caching a CEK and not cache it if the value is zero. This will avoid duplicate caching and possible user confusion when they are trying to configure key caching. The time-to-live value for the cache can be set with the `SQLServerColumnEncryptionKeyStoreProvider.setColumnEncryptionCacheTtl` method.

### Register a custom column master key store provider

This section applies to JDBC driver version 10.2 and higher.

Custom master key store providers can be registered with the driver at three different layers. The precedence of the three registrations is as follows:

- The per-statement registration is checked if it isn't empty.
- If the per-statement registration is empty, the per-connection registration is checked if it isn't empty.
- If the per-connection registration is empty, the global registration is checked.

Once any key store provider is found at a registration level, the driver will **NOT** fall back to the other registrations to search for a provider. If providers are registered but the proper provider isn't found at a level, an exception is thrown that contains only the registered providers in the registration that was checked.

The built-in column master key store provider that is available for the Windows Certificate Store is pre-registered. The Microsoft Java Keystore provider and Azure Key Vault Keystore provider can be implicitly pre-registered with a connection instance if credentials are provided in advance.

The three registration levels support different scenarios when querying encrypted data. The appropriate method can be used to ensure that a user of an application can access the plaintext data. Access to the unencrypted data only happens if they can provide the required column master key, by authenticating against the key store containing the column master key.

Applications that share a `SQLServerConnection` instance between multiple users might want to use `SQLServerStatement.registerColumnEncryptionKeyStoreProvidersOnStatement`. Each user must register a key store provider on a `SQLServerStatement` instance before executing a query to access an encrypted column. If the key store provider is able to access the required column master key in the key store that uses the user's given credentials, the query will succeed.

Applications that create a `SQLServerConnection` instance for each user might want to use `SQLServerConnection.registerColumnEncryptionKeyStoreProvidersOnConnection`. Key store providers registered with this method can be used by the connection for any query accessing encrypted data.

Key store providers registered with `SQLServerConnection.registerColumnEncryptionKeyStoreProviders` will use the identity given by the application when authenticating against the key store.

The following example shows the precedence of custom column master key store providers registered on a connection instance:

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> customKeyStoreProviders = new HashMap<>();
MyCustomKeyStore myProvider = new MyCustomKeyStore();
customKeyStoreProviders.put(myProvider.getName(), myProvider);
// Registers the provider globally
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(customKeyStoreProviders);

try (SQLServerConnection conn = getConnection()) {
    customKeyStoreProviders.clear();
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    customKeyStoreProviders.put(akvProvider.getName(), akvProvider);
    
    // Registers the provider on the connection
    // These providers will take precedence over globally registered providers
    conn.registerColumnEncryptionKeyStoreProvidersOnConnection(customKeyStoreProviders);              
}
```

The following example shows the precedence of custom column master key store providers registered on a statement instance:

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> customKeyStoreProviders = new HashMap<>();
MyCustomKeyStore firstProvider = new MyCustomKeyStore();
customKeyStoreProviders.put("FIRST_CUSTOM_STORE", firstProvider);
// Registers the provider globally
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(customKeyStoreProviders);

try (SQLServerConnection conn = getConnection()) {
    customKeyStoreProviders.clear();
    MyCustomKeyStore secondProvider = new MyCustomKeyStore();
    customKeyStoreProviders.put("SECOND_CUSTOM_STORE", secondProvider);    
    // Registers the provider on the connection
    conn.registerColumnEncryptionKeyStoreProvidersOnConnection(customKeyStoreProviders);

    try (SQLServerStatement stmt = (SQLServerStatement) conn.createStatement()) {
        customKeyStoreProviders.clear();
        SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
        customKeyStoreProviders.put(akvProvider.getName(), akvProvider);

        // Registers the provider on the statement
        // These providers will take precedence over connection-level providers and globally registered providers
        stmt.registerColumnEncryptionKeyStoreProvidersOnStatement(customKeyStoreProviders);
    }             
}
```

## Use column master key store providers for programmatic key provisioning

To access encrypted columns, the Microsoft JDBC Driver for SQL Server transparently finds and calls the right column master key store provider to decrypt column encryption keys. Typically, your normal application code doesn't directly call column master key store providers. You may, however, instantiate and call a provider programmatically to provision and manage Always Encrypted keys. This step may be done to generate an encrypted column encryption key and decrypt a column encryption key as part column master key rotation, for example. For more information, see [Overview of Key Management for Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

If you use a custom keystore provider, implementing your own key management tools may be required. To use keys stored in Windows Certificate Store or in Azure Key Vault, you can use existing tools, such as SQL Server Management Studio or PowerShell, to manage and provision keys. To use keys stored in the Java Key Store, you need to provision keys programmatically. The following example illustrates how to use the `SQLServerColumnEncryptionJavaKeyStoreProvider` class to encrypt the key with a key stored in the Java Key Store.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://learn.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## Enabling Always Encrypted for application queries

The easiest way to enable the encryption of parameters and the decryption of query results of encrypted columns is by setting the value of the **`columnEncryptionSetting`** connection string keyword to **`Enabled`**.

The following connection string is an example of enabling Always Encrypted in the JDBC driver:

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;encrypt=true;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

The following code is an equivalent example to use the `SQLServerDataSource` object:

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

Always Encrypted can also be enabled for individual queries. For more information, see [Controlling the performance impact of Always Encrypted](#controlling-the-performance-impact-of-always-encrypted). Enabling Always Encrypted isn't sufficient for encryption or decryption to succeed. You also need to make sure:

- The application has the _`VIEW ANY COLUMN MASTER KEY DEFINITION`_ and _`VIEW ANY COLUMN ENCRYPTION KEY DEFINITION`_ database permissions, required to access the metadata about Always Encrypted keys in the database. For details, see [Permissions in Always Encrypted (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions).
- The application can access the column master key that protects the column encryption keys, which encrypt the queried database columns. To use the Java Key Store provider, you need to provide extra credentials in the connection string. For more information, see [Use Java Key Store provider](#use-java-key-store-provider).

### Configuring how java.sql.Time values are sent to the server

The **`sendTimeAsDatetime`** connection property is used to configure how the java.sql.Time value is sent to the server. When set to false, the time value is sent as a SQL Server time type. When set to true, the time value is sent as a datetime type. If a time column is encrypted, the **`sendTimeAsDatetime`** property must be false, as encrypted columns don't support the conversion from time to datetime. Also note that this property is by default true, so to use encrypted time columns set it to false. Otherwise, the driver will throw an exception. Starting with version 6.0 of the driver, the `SQLServerConnection` class has two methods to configure the value of this property programmatically:

- public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
- public boolean getSendTimeAsDatetime()

For more information on this property, see [Configuring How java.sql.Time Values are Sent to the Server](configuring-how-java-sql-time-values-are-sent-to-the-server.md).

### Configuring how String values are sent to the server

The **`sendStringParametersAsUnicode`** connection property is used to configure how String values are sent to SQL Server. If set to true, String parameters are sent to the server in Unicode format. If set to false, String parameters are sent in non-Unicode format, such as ASCII or MBCS, instead of Unicode. The default value for this property is true. When Always Encrypted is enabled and a `char`/`varchar`/`varchar(max)` column is encrypted, the value of **`sendStringParametersAsUnicode`** must be set to false. If this property is set to true, the driver will throw an exception when decrypting data from an encrypted `char`/`varchar`/`varchar(max)` column that has Unicode characters. For more information on this property, see [Setting the Connection Properties](setting-the-connection-properties.md).

> [!IMPORTANT]
> If `sendStringParametersAsUnicode` is set to `true` and unicode data is inserted into a `char`/`varchar` column encrypted with Always Encrypted, data loss may occur without an error being reported. The data loss may only be detected when trying to decrypt the data after reading it back from the server. An error like `Decryption failed. The last 10 bytes of the encrypted column encryption key are: 'C3-D9-10-4E-C1-45-8B-94-A2-43'. The first 10 bytes of ciphertext are: '01-9B-9D-A6-3E-40-22-53-15-9B'.` might be the result.
>
> It is important to use correct column data types and specify the correct data type for parameters when inserting encrypted data. If unicode data is expected, use `nchar`/`nvarchar` columns and `setNString()` methods. The server can't perform implicit data conversions and has limited ability to detect data errors when Always Encrypted is enabled.

## Retrieving and modifying data in encrypted columns

Once you enable Always Encrypted for application queries, you can use standard JDBC APIs to retrieve or modify data in encrypted database columns. If your application has the required database permissions and can access the column master key, the driver will encrypt any query parameters that target encrypted columns, and decrypt data that's retrieved from encrypted columns.

If Always Encrypted isn't enabled, queries with parameters that target encrypted columns will fail. Queries can still retrieve data from encrypted columns as long as the query has no parameters targeting encrypted columns. However, the driver won't attempt to decrypt any values that are retrieved from encrypted columns and the application will receive binary encrypted data (as byte arrays).

The following table summarizes the behavior of queries depending on whether Always Encrypted is enabled or not:

| Query characteristic                                                                           | Always Encrypted is enabled and application can access the keys and key metadata                                                                                                                        | Always Encrypted is enabled and application can't access the keys or key metadata | Always Encrypted is disabled                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Queries with parameters targeting encrypted columns.                                           | Parameter values are transparently encrypted.                                                                                                                                                           | Error                                                                             | Error                                                                                                               |
| Queries retrieving data from encrypted columns without parameters targeting encrypted columns. | Results from encrypted columns are transparently decrypted. The application receives plaintext values of the JDBC datatypes corresponding to the SQL Server types configured for the encrypted columns. | Error                                                                             | Results from encrypted columns aren't decrypted. The application receives encrypted values as byte arrays (byte[]). |

### Inserting and retrieving encrypted data examples

The following examples illustrate retrieving and modifying data in encrypted columns. The examples assume the target table with the following schema and encrypted SSN and BirthDate columns. If you've configured a Column Master Key named "MyCMK" and a Column Encryption Key named "MyCEK" (as described in the preceding keystore providers sections), you can create the table with this script:

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY]);
 GO
```

For each Java code example, you'll need to insert keystore-specific code in the location noted.

To use an Azure Key Vault keystore provider:

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

To use a Windows Certificate Store keystore provider:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

To use a Java Key Store keystore provider:

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### Inserting data example

This example inserts a row into the Patients table. Note the following items:

- There's nothing specific to encryption in the sample code. The Microsoft JDBC Driver for SQL Server automatically detects and encrypts the parameters that target encrypted columns. This behavior makes encryption transparent to the application.
- The values inserted into database columns, including the encrypted columns, are passed as parameters with `SQLServerPreparedStatement`. While parameters are optional when sending values to non-encrypted columns (although, it's highly recommended because it helps prevent SQL injection), it's required for values that target encrypted columns. If the values inserted into the encrypted columns were passed as literals embedded in the query statement, the query would fail because the driver wouldn't be able to determine the values in the target encrypted columns and it wouldn't encrypt the values. As a result, the server would reject them as incompatible with the encrypted columns.
- All values printed by the program will be in plaintext, as the Microsoft JDBC Driver for SQL Server will transparently decrypt the data retrieved from the encrypted columns.
- If you're doing a lookup with a WHERE clause, the value that's used in the WHERE clause needs to be passed as a parameter so that the driver can transparently encrypt it before sending it to the database. In the following example, the SSN is passed as a parameter but the LastName is passed as a literal as LastName isn't encrypted.
- The setter method used for the parameter targeting the SSN column is `setString()`, which maps to the `char`/`varchar` SQL Server data type. If for this parameter, the setter method used was `setNString()`, which maps to `nchar`/`nvarchar`, the query would fail, as Always Encrypted doesn't support conversions from encrypted `nchar`/`nvarchar` values to encrypted `char`/`varchar` values.

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### Retrieving plaintext data example

The following example demonstrates filtering data based on encrypted values and retrieving plaintext data from encrypted columns. Note the following items:

- The value that's used in the WHERE clause to filter on the SSN column needs to be passed as a parameter so that the Microsoft JDBC Driver for SQL Server can transparently encrypt it before sending it to the database.
- All values printed by the program will be in plaintext, as the Microsoft JDBC Driver for SQL Server will transparently decrypt the data retrieved from the SSN and BirthDate columns.

> [!NOTE]
> if columns are encrypted with deterministic encryption, queries can perform equality comparisons on them. For more information, see [deterministic encryption](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption).

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### Retrieving encrypted data example

If Always Encrypted isn't enabled, a query can still retrieve data from encrypted columns, as long as the query has no parameters targeting encrypted columns.

The following example illustrates retrieving binary encrypted data from encrypted columns. Note the following items:

- Since Always Encrypted isn't enabled in the connection string, the query will return encrypted values of SSN and BirthDate as byte arrays (the program converts the values to strings).
- A query retrieving data from encrypted columns with Always Encrypted disabled can have parameters, as long as none of the parameters target an encrypted column. The following query filters by LastName, which isn't encrypted in the database. If the query filtered by SSN or BirthDate, the query would fail.

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### Avoiding common problems when querying encrypted columns

This section describes common categories of errors when querying encrypted columns from Java applications and a few guidelines on how to avoid them.

### Unsupported data type conversion errors

Always Encrypted supports few conversions for encrypted data types. See [Always Encrypted (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) for the detailed list of supported type conversions. Here's what you can do to avoid data type conversion errors. Make sure that:

- you use the proper setter methods when passing values for parameters that target encrypted columns. Ensure that the SQL Server data type of the parameter is exactly the same as the type of the target column or a conversion of the SQL Server data type of the parameter to the target type of the column is supported. API methods have been added to the `SQLServerPreparedStatement`, `SQLServerCallableStatement`, and `SQLServerResultSet` classes to pass parameters corresponding to specific SQL Server data types. For a complete list of new APIs, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md). Failing to comply with data type definitions will likely result in operand type clash errors. The following are some examples of adjustments that may be needed when using Always Encrypted:
  - You can use the `setTimestamp()` method to pass a parameter to a non-encrypted datetime2 or datetime column. But when a column is encrypted you have to use the exact method representing the type of the column in the database. Use `setTimestamp()` to pass values to an encrypted datetime2 column and use `setDateTime()` to pass values to an encrypted datetime column.
  - You can use the `setBinary()` method to pass a parameter to a non-encrypted `varbinary(max)` or `binary` column. The driver defaults to the `BINARY` data type for `setBinary()` parameters and the server can implicitly convert the data to insert into a `varbinary(max)` column. But when a `varbinary(max)` column is encrypted you have to specify a more exact type for the parameter data. Example: `preparedStatement.setObject(1, binaryData, java.sql.JDBCType.LONGVARBINARY)`
- the precision and scale of parameters targeting columns of the decimal and numeric SQL Server data types is the same as the precision and scale configured for the target column. API methods have been added to the `SQLServerPreparedStatement`, `SQLServerCallableStatement`, and `SQLServerResultSet` classes to accept precision and scale along with data values for parameters/columns representing decimal and numeric data types. See [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md) for a complete list of new/overloaded APIs.
  - For example, When you're using Java's `BigDecimal` as the parameter type targeting a specified decimal column in the database, you need to supply the precision and scale to either the `setBigDecimal()` method or `setValue()` method. Failure to specify the correct precision and scale can result in an error like the following:

  ```java
  Operand type clash: decimal(18,0) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'myCek', column_encryption_key_database_name = 'issue2169') is incompatible with decimal(20,4) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'myCek', column_encryption_key_database_name = 'myDatabase')
  ```

- the fractional seconds precision/scale of parameters targeting columns of `datetime2`, `datetimeoffset`, or time SQL Server data types isn't greater than the fractional seconds precision/scale for the target column in queries that modify values of the target column. API methods have been added to the `SQLServerPreparedStatement`, `SQLServerCallableStatement`, and `SQLServerResultSet` classes to accept fractional seconds precision/scale along with data values for parameters representing these data types. For a complete list of new/overloaded APIs, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md).

### Errors due to incorrect connection properties

This section describes how to configure connection settings properly to use Always Encrypted data. Since encrypted data types support limited conversions, the **`sendTimeAsDatetime`** and **`sendStringParametersAsUnicode`** connection settings need proper configuration to use encrypted columns. Make sure that:

- [sendTimeAsDatetime](setting-the-connection-properties.md) connection setting is set to false when inserting data into encrypted time columns. For more information, see [Configuring how java.sql.Time Values are sent to the server](configuring-how-java-sql-time-values-are-sent-to-the-server.md).
- [sendStringParametersAsUnicode](setting-the-connection-properties.md) connection setting is set to true (or is left as the default) when inserting data into encrypted char/varchar/varchar(max) columns.

### Errors due to passing plaintext instead of encrypted values

Any value that targets an encrypted column needs to be encrypted inside the application. An attempt to insert/modify or to filter by a plaintext value on an encrypted column will result in an error similar to this one:

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

To prevent such errors, make sure:

- Always Encrypted is enabled for application queries targeting encrypted columns (for the connection string or for a specific query).
- you use prepared statements and parameters to send data targeting encrypted columns. The following example shows a query that incorrectly filters by a literal/constant on an encrypted column (SSN), instead of passing the literal inside as a parameter. This query will fail:

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## Force encryption on input parameters

The Force Encryption feature enforces encryption of a parameter with Always Encrypted. If force encryption is used and SQL Server informs the driver that the parameter doesn't need to be encrypted, the query that uses the parameter will fail. This property provides added protection against security attacks that involve a compromised SQL Server providing incorrect encryption metadata to the client, which may lead to data disclosure. The set* methods in the `SQLServerPreparedStatement` and `SQLServerCallableStatement` classes and the `update*` methods in the `SQLServerResultSet` class are overloaded to accept a boolean argument to specify the force encryption setting. If the value of this argument is false, the driver won't force encryption on parameters. If force encryption is set to true, the query parameter is only sent if the destination column is encrypted and Always Encrypted is enabled on the connection or on the statement. This property gives an extra layer of security, ensuring that the driver doesn't mistakenly send data to SQL Server as plaintext when it's expected to be encrypted.

For more information on the `SQLServerPreparedStatement` and `SQLServerCallableStatement` methods that are overloaded with the force encryption setting, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md)

## Controlling the performance impact of Always Encrypted

Because Always Encrypted is a client-side encryption technology, most of the performance overhead is observed on the client side, not in the database. Apart from the cost of encryption and decryption operations, other sources of performance overheads on the client side are:

- Added round trips to the database to retrieve metadata for query parameters.
- Calls to a column master key store to access a column master key.

This section describes the built-in performance optimizations in the Microsoft JDBC Driver for SQL Server and how you can control the impact of the above two factors on performance.

### Controlling round trips to retrieve metadata for query parameters

If Always Encrypted is enabled for a connection, by default the driver will call [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) for each parameterized query, passing the query statement (without any parameter values) to the database. [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) analyzes the query statement to find out if any parameters need to be encrypted, and if so, for each one it returns the encryption-related information that allows the driver to encrypt parameter values. This behavior ensures a high level of transparency to the client application. As long as the application uses parameters to pass values that target encrypted columns to the driver, the application (and the application developer) doesn't need to know which queries access encrypted columns.

### Setting Always Encrypted at the query level

To control the performance impact of retrieving encryption metadata for parameterized queries, you can enable Always Encrypted for individual queries instead of setting it up for the connection. This way you can ensure that sys.sp_describe_parameter_encryption is invoked only for queries that you know have parameters targeting encrypted columns. Note, however, that by doing so you reduce the transparency of encryption: if you change encryption properties of your database columns, you may need to change the code of your application to align it with the schema changes.

To control the Always Encrypted behavior of individual queries, you need to configure individual statement objects by passing an Enum, SQLServerStatementColumnEncryptionSetting, which specifies how data will be sent and received when reading and writing encrypted columns for that specific statement. Here are some useful guidelines:

- If most queries a client application sends over a database connection access encrypted columns, use these guidelines:
  - Set the **`columnEncryptionSetting`** connection string keyword to **`Enabled`**.
  - Set `SQLServerStatementColumnEncryptionSetting.Disabled` for individual queries that don't access any encrypted columns. This setting will disable both calling `sys.sp_describe_parameter_encryption` and decrypting any values in the result set.
  - Set `SQLServerStatementColumnEncryptionSetting.ResultSet` for individual queries that don't have any parameters requiring encryption but retrieve data from encrypted columns. This setting will disable calling `sys.sp_describe_parameter_encryption` and parameter encryption. The query will decrypt the results from encryption columns.

- If most queries a client application sends over a database connection don't access encrypted columns, use these guidelines:
  - Set the **`columnEncryptionSetting`** connection string keyword to **`Disabled`**.
  - Set `SQLServerStatementColumnEncryptionSetting.Enabled` for individual queries that have any parameters that need to be encrypted. This setting will enable both calling `sys.sp_describe_parameter_encryption` and decrypting of any query results retrieved from encrypted columns.
  - Set `SQLServerStatementColumnEncryptionSetting.ResultSet` for queries that don't have any parameters requiring encryption but retrieve data from encrypted columns. This setting will disable calling `sys.sp_describe_parameter_encryption` and parameter encryption. The query will decrypt the results from encryption columns.

The `SQLServerStatementColumnEncryptionSetting` settings can't be used to bypass encryption and gain access to plaintext data. For more information on how to configure column encryption on a statement, see [Always Encrypted API Reference for the JDBC Driver](always-encrypted-api-reference-for-the-jdbc-driver.md).

In the following example, Always Encrypted is disabled for the database connection. The query the application issues has a parameter that targets the LastName column that isn't encrypted. The query retrieves data from the SSN and BirthDate columns that are both encrypted. In such a case, calling `sys.sp_describe_parameter_encryption` to retrieve encryption metadata isn't required. However, the decryption of the query results needs to be enabled so that the application can receive plaintext values from the two encrypted columns. The `SQLServerStatementColumnEncryptionSetting.ResultSet` setting is used to ensure that.

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;encrypt=true;databaseName=<database>;user=<user>;password=<password>;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>"
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### Query parameter metadata caching

To reduce the number of round trips to the database, the Microsoft JDBC Driver for SQL Server can cache encryption-related information for query parameters. As of version 11.2.0, encryption-related information for parameters returned from [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) calls will be cached by the driver if the associated SQL Server process doesn't use secure enclaves. For caching with the use of secure enclaves, the server must support re-establishing of the enclave session in cases where the session is no longer valid.

### Column encryption key caching

To reduce the number of calls to a column master key store to decrypt column encryption keys, the Microsoft JDBC Driver for SQL Server caches the plaintext column encryption keys in memory. After the driver receives the encrypted column encryption key value from the database metadata, the driver first tries to find the plaintext column encryption key corresponding to the encrypted key value. The driver calls the keystore containing the column master key only if it can't find the encrypted column encryption key value in the cache.

You can configure a time-to-live value for the column encryption key entries in the cache with the API, `setColumnEncryptionKeyCacheTtl()`, in the `SQLServerConnection` class. The default time-to-live value for the column encryption key entries in the cache is two hours. To turn off caching, use a value of 0. To set any time-to-live value, use the following API:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

For example, to set a time-to-live value of 10 minutes, use:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

Only DAYS, HOURS, MINUTES, or SECONDS are supported as the time unit.

## Copying encrypted data with SQLServerBulkCopy

With `SQLServerBulkCopy`, you can copy data that is already encrypted and stored in one table to another table without decrypting the data. To do that:

- Make sure the encryption configuration of the target table is identical to the configuration of the source table. In particular, both tables must have the same columns encrypted and the columns must be encrypted using the same encryption types and the same encryption keys. If any target column is encrypted differently than its corresponding source column, you won't be able to decrypt the data in the target table after the copy operation. The data will be corrupted.
- Configure both database connections to the source table and to the target table without Always Encrypted enabled.
- Set the `allowEncryptedValueModifications` option. For more information, see [Using bulk copy with the JDBC driver](using-bulk-copy-with-the-jdbc-driver.md).

> [!NOTE]
> Use caution when specifying `AllowEncryptedValueModifications` as this option may lead to corrupting the database because the Microsoft JDBC Driver for SQL Server doesn't check if the data is indeed encrypted or if it is correctly encrypted with the same encryption type, algorithm, and key as the target column.

## See also

[Always Encrypted (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
