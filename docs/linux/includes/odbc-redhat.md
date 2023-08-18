---
author: rwestMSFT
ms.author: randolphwest
ms.date: 07/11/2023
ms.service: sql
ms.topic: include
---
<a id="RHEL"></a>

Use the following steps to install the **mssql-tools18** on Red Hat Enterprise Linux.

1. Enter superuser mode.

   ```bash
   sudo su
   ```

1. Download the Microsoft Red Hat repository configuration file.

   - For Red Hat 8, use the following command:

     ```bash
     curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo
     ```

   - For Red Hat 7, use the following command:

     ```bash
     curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
     ```

1. Exit superuser mode.

   ```bash
   exit
   ```

1. If you had a previous version of **mssql-tools** installed, remove any older unixODBC packages.

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Run the following commands to install **mssql-tools18** with the unixODBC developer package.

   ```bash
   sudo yum install -y mssql-tools18 unixodbc-dev
   ```

   > [!NOTE]  
   > To update to the latest version of **mssql-tools**, run the following commands:
   >  
   > ```bash
   > sudo yum check-update
   > sudo yum update mssql-tools18
   > ```

1. **Optional**: Add `/opt/mssql-tools18/bin/` to your `PATH` environment variable in a bash shell.

   To make **sqlcmd** and **bcp** accessible from the bash shell for login sessions, modify your `PATH` in the `~/.bash_profile` file with the following command:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bash_profile
   ```

   To make **sqlcmd** and **bcp** accessible from the bash shell for interactive/non-login sessions, modify the `PATH` in the `~/.bashrc` file with the following command:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools18/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```
