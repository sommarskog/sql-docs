---
title: Configure SMB storage FCI - SQL Server on Linux
description: Learn to configure a failover cluster instance (FCI) using SMB storage for SQL Server on Linux.
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: vanto
ms.date: 08/28/2017
ms.service: sql
ms.subservice: linux
ms.topic: conceptual
---
# Configure failover cluster instance - SMB - SQL Server on Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

This article explains how to configure SMB storage for a failover cluster instance (FCI) on Linux. 
 
In the non-Windows world, SMB is often referred to as a Common Internet File System (CIFS) share and implemented via Samba. In the Windows world, accessing an SMB share is done this way: \\SERVERNAME\SHARENAME. For Linux-based SQL Server installations, the SMB share must be mounted as a folder.

## Important source and server information

Here are some tips and notes for successfully using SMB:
- The SMB share can be on Windows, Linux, or even from an appliance as long as it is using SMB 3.0 or higher. For more information on Samba and SMB 3.0, see [SMB 3.0](https://wiki.samba.org/index.php/Samba3/SMB2#SMB_3.0) to see if your Samba implementation is compliant with SMB 3.0.
- The SMB share should be highly available.
- Security must be set properly on the SMB share. Below is an example from /etc/samba/smb.conf, where SQLData1 is the name of the share.

![Screenshot showing that SQLData1 is the name of the share.][1]

## Instructions

1. Choose one of the servers that will participate in the FCI configuration. It does not matter which one.
   
1. Get information about the mssql user.
   
   ```bash
    sudo id mssql
   ```
   
   Note the uid, gid, and groups. 
   
1. Execute `sudo smbclient -L //NameOrIP/ShareName -U User`.
   
   \<NameOrIP> is the DNS name or IP address of the server hosting the SMB share.
   
   \<ShareName> is the name of the SMB share. 
   
1. For system databases or anything stored in the default data location follow these steps. Otherwise skip to step 5. 
   
   1. Ensure that SQL Server is stopped on the server that you are working on.
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Switch fully to be the superuser. You will not receive any acknowledgement if successful.
      
      ```bash
      sudo -i
      ```
      
   1. Switch to be the mssql user. You will not receive any acknowledgement if successful.
      
      ```bash
      su mssql
      ```
      
   1. Create a temporary directory to store the SQL Server data and log files. You will not receive any acknowledgement if successful.
      
      ```bash
      mkdir <TempDir>
      ```
      
      \<TempDir> is the name of the folder. The following example creates a folder named /var/opt/mssql/tmp.
      
      ```bash
      mkdir /var/opt/mssql/tmp
      ```
      
   1. Copy the SQL Server data and log files to the temporary directory. You will not receive any acknowledgement if successful.
      
      ```bash
      cp /var/opt/mssql/data/* <TempDir>
      ```
      
      \<TempDir> is the name of the folder from the previous step.
      
   1. Verify that the files are in the directory.
      
      ```bash
      ls <TempDir>
      ```
      
      \<TempDir> is the name of the folder from Step d.
      
   1. Delete the files from the existing SQL Server data directory. You will not receive any acknowledgement if successful.
      
      ```bash
      rm - f /var/opt/mssql/data/*
      ```
      
   1. Verify that the files have been deleted. 
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Type exit to switch back to the root user.
      
   1. Mount the SMB share in the SQL Server data folder. You will not receive any acknowledgement if successful. This example shows the syntax for connecting to a Windows Server-based SMB 3.0 share.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> /var/opt/mssql/data -o vers=3.0,username=<UserName>,password=<Password>,domain=<domain>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> is the name of the server with the SMB share
      
      \<ShareName> is the name of the share
      
      \<UserName> is the name of the user to access the share
      
      \<Password> is the password for the user
      
      \<domain> is the name of Active Directory
      
      \<mssqlUID> is the UID of the mssql user 
      
      \<mssqlGID> is the GID of the mssql user
      
   1. Check to see that the mount was successful by issuing mount with no switches.
      
      ```bash
      mount
      ```
      
   1. Switch to the mssql user. You will not receive any acknowledgement if successful.
      
      ```bash
      su mssql
      ```
      
   1. Copy the files from the temporary directory /var/opt/mssql/data. You will not receive any acknowledgement if successful.
      
      ```bash
      cp /var/opt/mssql/tmp/* /var/opt/mssql/data
      ```
      
   1. Verify the files are there.
      
      ```bash
      ls /var/opt/mssql/data
      ```
      
   1. Enter exit to not be mssql 
      
   1. Enter exit to not be root
   
   1. Start SQL Server. If everything was copied correctly and security applied correctly, SQL Server should show as started.
      
      ```bash
      sudo systemctl start mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. To test further, create a database to ensure the permissions are fine. The following example uses Transact-SQL; you can use SSMS.
      
      ![10_testcreatedb][2] 
      
   1. Stop SQL Server and verify it is shut down. If you are going to be adding or testing other disks, do not shut down SQL Server until those are added and tested.
      
      ```bash
      sudo systemctl stop mssql-server
      sudo systemctl status mssql-server
      ```
      
   1. Only if finished, unmount the share. If not, unmount after finishing testing/adding any additional disks.
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> is the IP address or name of the SMB host
      
      \<ShareName> is the name of the share
      
      \<FolderMountedIn> is the name of the folder where SMB is mounted
      
5. For things other than system databases, such as user databases or backups, follow these steps. If only using the default location, skip to Step 14.
   
   1. Switch to be the superuser. You will not receive any acknowledgement if successful.
      
      ```bash
      sudo -i
      ```
      
   1. Create a folder that will be used by SQL Server. 
      
      ```bash
      mkdir <FolderName>
      ```
      
      \<FolderName> is the name of the folder. The folder's full path needs to be specified if not in the right location. The following example creates a folder named /var/opt/mssql/userdata.
      
      ```bash
      mkdir /var/opt/mssql/userdata
      ```
      
   1. Mount the SMB share in the SQL Server data folder. You will not receive any acknowledgement if successful. This example shows the syntax for connecting to a Samba-based SMB 3.0 share.
      
      ```bash
      Mount -t cifs //<ServerName>/<ShareName> <FolderName> -o vers=3.0,username=<UserName>,password=<Password>,uid=<mssqlUID>,gid=<mssqlGID>,file_mode=0777,dir_mode=0777
      ```
      
      \<ServerName> is the name of the server with the SMB share
      
      \<ShareName> is the name of the share
      
      \<FolderName> is the name of the folder created in the last step  
      
      \<UserName> is the name of the user to access the share
      
      \<Password> is the password for the user
      
      \<mssqlUID> is the UID of the mssql user
      
      \<mssqlGID> is the GID of the mssql user.
      
   1. Check to see that the mount was successful by issuing mount with no switches.
   
   1. Type exit to no longer be the superuser.
   
   1. To test, create a database in that folder. The following example uses sqlcmd to create a database, switch context to it, verify the files exist at the OS level, and then deletes the temporary location. You can use SSMS.
   
   1. Unmount the share 
      
      ```bash
      sudo umount //<IPAddressorServerName>/<ShareName> /<FolderMountedIn>
      ```
      
      \<IPAddressOrServerName> is the IP address or name of the SMB host
      
      \<ShareName> is the name of the share
      
      \<FolderMountedIn> is the name of the folder where SMB is mounted.
   
1. Repeat the steps on the other node(s).

You are now ready to configure the FCI.

## Next steps

[Configure failover cluster instance - SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
[1]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/05-smbsource.png 
[2]: ./media/sql-server-linux-shared-disk-cluster-configure-smb/10-testcreatedb.png 
