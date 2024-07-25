## setup
### 1. clone repository
- https://github.com/oracle/docker-images.git

### 2. copy instance
- `docker-images/OracleDatabase/SingleInstance/dockerfiles/19.3.0`

### 3. ORACLE DATABASE software download 
- [オラクル・データベース・ソフトウェアのダウンロード](https://www.oracle.com/jp/database/technologies/oracle-database-software-downloads.html)
- [Oracle Database 19c for Linux x86-64](https://download.oracle.com/otn/linux/oracle19c/190000/LINUX.X64_193000_db_home.zip)

### 4. build image
```shell
$ ./buildContainerImage.sh -v 19.3.0 -e -i
# ...

#15 DONE 47.3s

What's Next?
  View a summary of image vulnerabilities and recommendations → docker scout quickview


  Oracle Database container image for 'ee' version 19.3.0 is ready to be extended:

    --> oracle/database:19.3.0-ee

  Build completed in 676 seconds.

```

### 5. `docker-compose.yml` setting
```yml
services:
  oracle-database-19.3.0-ee:
    image: oracle/database:19.3.0-ee
    container_name: oracle-database-19.3.0-ee
    ports:
      - 1521:1521
      - 5500:5500
      - 8080:8080
    volumes:
      - ./dump:/opt/oracle/dump
      - ./oradata:/opt/oracle/oradata
      - ./startup:/opt/oracle/scripts/startup
    environment:
      ORACLE_SID: ORCLCDB
      ORACLE_PDB: ORCLPDB1
      ORACLE_PWD: oracle
```

### 6. container build
```shell
$ docker-compose up -d --build
 Network oracle-master_default  Creating
 Network oracle-master_default  Created
 Container oracle-database-19.3.0-ee  Creating
 Container oracle-database-19.3.0-ee  Created
 Container oracle-database-19.3.0-ee  Starting
 Container oracle-database-19.3.0-ee  Started
```

**initiale setup log**

```log
2024-06-16 13:57:19 ORACLE EDITION: ENTERPRISE
2024-06-16 13:57:20 
2024-06-16 13:57:20 LSNRCTL for Linux: Version 19.0.0.0.0 - Production on 16-JUN-2024 04:57:20
2024-06-16 13:57:20 
2024-06-16 13:57:20 Copyright (c) 1991, 2019, Oracle.  All rights reserved.
2024-06-16 13:57:20 
2024-06-16 13:57:20 Starting /opt/oracle/product/19c/dbhome_1/bin/tnslsnr: please wait...
2024-06-16 13:57:20 
2024-06-16 13:57:20 TNSLSNR for Linux: Version 19.0.0.0.0 - Production
2024-06-16 13:57:20 System parameter file is /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
2024-06-16 13:57:20 Log messages written to /opt/oracle/diag/tnslsnr/336bc44674d8/listener/alert/log.xml
2024-06-16 13:57:20 Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
2024-06-16 13:57:20 Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
2024-06-16 13:57:20 
2024-06-16 13:57:20 Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
2024-06-16 13:57:20 STATUS of the LISTENER
2024-06-16 13:57:20 ------------------------
2024-06-16 13:57:20 Alias                     LISTENER
2024-06-16 13:57:20 Version                   TNSLSNR for Linux: Version 19.0.0.0.0 - Production
2024-06-16 13:57:20 Start Date                16-JUN-2024 04:57:20
2024-06-16 13:57:20 Uptime                    0 days 0 hr. 0 min. 0 sec
2024-06-16 13:57:20 Trace Level               off
2024-06-16 13:57:20 Security                  ON: Local OS Authentication
2024-06-16 13:57:20 SNMP                      OFF
2024-06-16 13:57:20 Listener Parameter File   /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
2024-06-16 13:57:20 Listener Log File         /opt/oracle/diag/tnslsnr/336bc44674d8/listener/alert/log.xml
2024-06-16 13:57:20 Listening Endpoints Summary...
2024-06-16 13:57:20   (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
2024-06-16 13:57:20   (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
2024-06-16 13:57:20 The listener supports no services
2024-06-16 13:57:20 The command completed successfully
2024-06-16 13:57:31 [WARNING] [DBT-06208] The 'SYS' password entered does not conform to the Oracle recommended standards.
2024-06-16 13:57:31    CAUSE: 
2024-06-16 13:57:31 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 13:57:31 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 13:57:31    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 13:57:31 [WARNING] [DBT-06208] The 'SYSTEM' password entered does not conform to the Oracle recommended standards.
2024-06-16 13:57:31    CAUSE: 
2024-06-16 13:57:31 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 13:57:31 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 13:57:31    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 13:57:31 [WARNING] [DBT-06208] The 'PDBADMIN' password entered does not conform to the Oracle recommended standards.
2024-06-16 13:57:31    CAUSE: 
2024-06-16 13:57:31 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 13:57:31 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 13:57:31    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 13:57:33 Prepare for db operation
2024-06-16 13:57:33 8% complete
2024-06-16 13:57:33 Copying database files
2024-06-16 13:59:27 31% complete
2024-06-16 13:59:27 Creating and starting Oracle instance
2024-06-16 13:59:59 32% complete
2024-06-16 14:00:16 36% complete
2024-06-16 14:08:17 ORACLE EDITION: ENTERPRISE
2024-06-16 14:08:17 
2024-06-16 14:08:17 LSNRCTL for Linux: Version 19.0.0.0.0 - Production on 16-JUN-2024 05:08:17
2024-06-16 14:08:17 
2024-06-16 14:08:17 Copyright (c) 1991, 2019, Oracle.  All rights reserved.
2024-06-16 14:08:17 
2024-06-16 14:08:19 Starting /opt/oracle/product/19c/dbhome_1/bin/tnslsnr: please wait...
2024-06-16 14:08:19 
2024-06-16 14:08:19 TNSLSNR for Linux: Version 19.0.0.0.0 - Production
2024-06-16 14:08:19 System parameter file is /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
2024-06-16 14:08:19 Log messages written to /opt/oracle/diag/tnslsnr/336bc44674d8/listener/alert/log.xml
2024-06-16 14:08:19 Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
2024-06-16 14:08:19 Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
2024-06-16 14:08:19 
2024-06-16 14:08:19 Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
2024-06-16 14:08:19 STATUS of the LISTENER
2024-06-16 14:08:19 ------------------------
2024-06-16 14:08:19 Alias                     LISTENER
2024-06-16 14:08:19 Version                   TNSLSNR for Linux: Version 19.0.0.0.0 - Production
2024-06-16 14:08:19 Start Date                16-JUN-2024 05:08:19
2024-06-16 14:08:19 Uptime                    0 days 0 hr. 0 min. 0 sec
2024-06-16 14:08:19 Trace Level               off
2024-06-16 14:08:19 Security                  ON: Local OS Authentication
2024-06-16 14:08:19 SNMP                      OFF
2024-06-16 14:08:19 Listener Parameter File   /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
2024-06-16 14:08:19 Listener Log File         /opt/oracle/diag/tnslsnr/336bc44674d8/listener/alert/log.xml
2024-06-16 14:08:19 Listening Endpoints Summary...
2024-06-16 14:08:19   (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
2024-06-16 14:08:19   (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
2024-06-16 14:08:19 The listener supports no services
2024-06-16 14:08:19 The command completed successfully
2024-06-16 14:08:37 [WARNING] [DBT-06208] The 'SYS' password entered does not conform to the Oracle recommended standards.
2024-06-16 14:08:37    CAUSE: 
2024-06-16 14:08:37 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 14:08:37 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 14:08:37    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 14:08:37 [WARNING] [DBT-06208] The 'SYSTEM' password entered does not conform to the Oracle recommended standards.
2024-06-16 14:08:37    CAUSE: 
2024-06-16 14:08:37 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 14:08:37 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 14:08:37    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 14:08:37 [WARNING] [DBT-06208] The 'PDBADMIN' password entered does not conform to the Oracle recommended standards.
2024-06-16 14:08:37    CAUSE: 
2024-06-16 14:08:37 a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
2024-06-16 14:08:37 b.The password entered is a keyword that Oracle does not recommend to be used as password
2024-06-16 14:08:37    ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
2024-06-16 14:08:39 Prepare for db operation
2024-06-16 14:08:40 8% complete
2024-06-16 14:08:40 Copying database files
2024-06-16 14:10:49 31% complete
2024-06-16 14:10:49 Creating and starting Oracle instance
2024-06-16 14:11:22 32% complete
2024-06-16 14:11:36 36% complete
2024-06-16 14:18:52 40% complete
2024-06-16 14:18:53 43% complete
2024-06-16 14:19:56 46% complete
2024-06-16 14:19:56 Completing Database Creation
2024-06-16 14:23:01 51% complete
2024-06-16 14:26:14 54% complete
2024-06-16 14:26:14 Creating Pluggable Databases
2024-06-16 14:26:30 58% complete
2024-06-16 14:26:30 77% complete
2024-06-16 14:26:30 Executing Post Configuration Actions
2024-06-16 14:26:30 100% complete
2024-06-16 14:26:30 Database creation complete. For details check the logfiles at:
2024-06-16 14:26:30  /opt/oracle/cfgtoollogs/dbca/ORCLCDB.
2024-06-16 14:26:30 Database Information:
2024-06-16 14:26:30 Global Database Name:ORCLCDB
2024-06-16 14:26:30 System Identifier(SID):ORCLCDB
2024-06-16 14:26:30 Look at the log file "/opt/oracle/cfgtoollogs/dbca/ORCLCDB/ORCLCDB.log" for further details.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL*Plus: Release 19.0.0.0.0 - Production on Sun Jun 16 05:26:30 2024
2024-06-16 14:26:30 Version 19.3.0.0.0
2024-06-16 14:26:30 
2024-06-16 14:26:30 Copyright (c) 1982, 2019, Oracle.  All rights reserved.
2024-06-16 14:26:30 
2024-06-16 14:26:30 
2024-06-16 14:26:30 Connected to:
2024-06-16 14:26:30 Oracle Database 19c Enterprise Edition Release 19.0.0.0.0 - Production
2024-06-16 14:26:30 Version 19.3.0.0.0
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 System altered.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 System altered.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 Pluggable database altered.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 PL/SQL procedure successfully completed.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> SQL> 
2024-06-16 14:26:30 Session altered.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 User created.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 Grant succeeded.
2024-06-16 14:26:30 
2024-06-16 14:26:30 SQL> 
2024-06-16 14:26:30 Grant succeeded.
2024-06-16 14:26:30 
2024-06-16 14:26:31 SQL> 
2024-06-16 14:26:31 Grant succeeded.
2024-06-16 14:26:31 
2024-06-16 14:26:31 SQL> 
2024-06-16 14:26:31 User altered.
2024-06-16 14:26:31 
2024-06-16 14:26:31 SQL> SQL> Disconnected from Oracle Database 19c Enterprise Edition Release 19.0.0.0.0 - Production
2024-06-16 14:26:31 Version 19.3.0.0.0
2024-06-16 14:26:31 The Oracle base remains unchanged with value /opt/oracle
2024-06-16 14:26:33 The Oracle base remains unchanged with value /opt/oracle
2024-06-16 14:26:35 #########################
2024-06-16 14:26:35 DATABASE IS READY TO USE!
2024-06-16 14:26:35 #########################
2024-06-16 14:26:36 The following output is now a tail of the alert.log:
2024-06-16 14:26:36 ORCLPDB1(3):ALTER DATABASE DEFAULT TABLESPACE "USERS"
2024-06-16 14:26:36 ORCLPDB1(3):Completed: ALTER DATABASE DEFAULT TABLESPACE "USERS"
2024-06-16 14:26:36 2024-06-16T05:26:30.570357+00:00
2024-06-16 14:26:36 ALTER SYSTEM SET control_files='/opt/oracle/oradata/ORCLCDB/control01.ctl' SCOPE=SPFILE;
2024-06-16 14:26:36 2024-06-16T05:26:30.586435+00:00
2024-06-16 14:26:36 ALTER SYSTEM SET local_listener='' SCOPE=BOTH;
2024-06-16 14:26:36    ALTER PLUGGABLE DATABASE ORCLPDB1 SAVE STATE
2024-06-16 14:26:36 Completed:    ALTER PLUGGABLE DATABASE ORCLPDB1 SAVE STATE
2024-06-16 14:26:36 
2024-06-16 14:26:36 XDB initialized.
2024-06-16 14:27:14 2024-06-16T05:27:13.309966+00:00
2024-06-16 14:27:14 TABLE SYS.WRP$_REPORTS: ADDED INTERVAL PARTITION SYS_P201 (5281) VALUES LESS THAN (TO_DATE(' 2024-06-17 01:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
2024-06-16 14:27:14 TABLE SYS.WRP$_REPORTS_DETAILS: ADDED INTERVAL PARTITION SYS_P202 (5281) VALUES LESS THAN (TO_DATE(' 2024-06-17 01:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
2024-06-16 14:27:14 TABLE SYS.WRP$_REPORTS_TIME_BANDS: ADDED INTERVAL PARTITION SYS_P205 (5280) VALUES LESS THAN (TO_DATE(' 2024-06-16 01:00:00', 'SYYYY-MM-DD HH24:MI:SS', 'NLS_CALENDAR=GREGORIAN'))
```

## option - X Server setup
ホストOS上に X Server を立てていく

### 1. `VcXsrv` をインストール

- https://sourceforge.net/projects/vcxsrv/

**windows10 で利用できる X Server**

| ソフトウェア | 概要 |
| -- | -- |
| VcXsrv | フリーのXサーバ |
| Cygwin/X | フリーのXサーバ。UNIX互換環境のCygwinの一つとして提供されている |
| Xming | 以前は無償だったXサーバ。現在では利用形態に応じていくらか支払う必要がある |
| MobaXterm | sshクライアント／ターミナル機能などが統合されているXサーバ製品。機能限定の無償版もある |
| X410 | Microsoft Storeで販売されている有償のXサーバ。ストアアプリなので、導入やバージョンアップなどが容易 |

### 2. oracle linux に xeyes X Client をインストール

```sh
$ docker exec -u root -ti oracle-database bash
bash-4.2# yum install -y xeyes
Loaded plugins: ovl
ol7_latest                                                                        | 3.6 kB  00:00:00
(1/3): ol7_latest/x86_64/group_gz                                                 | 136 kB  00:00:00
(2/3): ol7_latest/x86_64/updateinfo                                               | 3.6 MB  00:00:00
(3/3): ol7_latest/x86_64/primary_db                                               |  52 MB  00:00:03
Resolving Dependencies
--> Running transaction check
---> Package xorg-x11-apps.x86_64 0:7.7-7.el7 will be installed
--> Processing Dependency: libpng15.so.15(PNG15_0)(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libXaw.so.7()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libXcursor.so.1()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libXft.so.2()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libfontconfig.so.1()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libfontenc.so.1()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libfreetype.so.6()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libpng15.so.15()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Processing Dependency: libxkbfile.so.1()(64bit) for package: xorg-x11-apps-7.7-7.el7.x86_64
--> Running transaction check
---> Package fontconfig.x86_64 0:2.13.0-4.3.el7 will be installed
--> Processing Dependency: dejavu-sans-fonts for package: fontconfig-2.13.0-4.3.el7.x86_64
--> Processing Dependency: fontpackages-filesystem for package: fontconfig-2.13.0-4.3.el7.x86_64
---> Package freetype.x86_64 0:2.8-14.el7_9.1 will be installed
---> Package libXaw.x86_64 0:1.0.13-4.el7 will be installed
--> Processing Dependency: libXpm.so.4()(64bit) for package: libXaw-1.0.13-4.el7.x86_64
---> Package libXcursor.x86_64 0:1.1.15-1.el7 will be installed
--> Processing Dependency: libXfixes.so.3()(64bit) for package: libXcursor-1.1.15-1.el7.x86_64
---> Package libXft.x86_64 0:2.3.2-2.el7 will be installed
---> Package libfontenc.x86_64 0:1.1.3-3.el7 will be installed
---> Package libpng.x86_64 2:1.5.13-8.el7 will be installed
---> Package libxkbfile.x86_64 0:1.0.9-3.el7 will be installed
--> Running transaction check
---> Package dejavu-sans-fonts.noarch 0:2.33-6.el7 will be installed
--> Processing Dependency: dejavu-fonts-common = 2.33-6.el7 for package: dejavu-sans-fonts-2.33-6.el7.noa
rch
---> Package fontpackages-filesystem.noarch 0:1.44-8.el7 will be installed
---> Package libXfixes.x86_64 0:5.0.3-1.el7 will be installed
---> Package libXpm.x86_64 0:3.5.12-2.el7_9 will be installed
--> Running transaction check
---> Package dejavu-fonts-common.noarch 0:2.33-6.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=========================================================================================================
 Package                           Arch             Version                   Repository            Size
=========================================================================================================
Installing:
 xorg-x11-apps                     x86_64           7.7-7.el7                 ol7_latest           307 k
Installing for dependencies:
 dejavu-fonts-common               noarch           2.33-6.el7                ol7_latest            64 k
 dejavu-sans-fonts                 noarch           2.33-6.el7                ol7_latest           1.4 M
 fontconfig                        x86_64           2.13.0-4.3.el7            ol7_latest           254 k
 fontpackages-filesystem           noarch           1.44-8.el7                ol7_latest           9.4 k
 freetype                          x86_64           2.8-14.el7_9.1            ol7_latest           380 k
 libXaw                            x86_64           1.0.13-4.el7              ol7_latest           191 k
 libXcursor                        x86_64           1.1.15-1.el7              ol7_latest            30 k
 libXfixes                         x86_64           5.0.3-1.el7               ol7_latest            18 k
 libXft                            x86_64           2.3.2-2.el7               ol7_latest            58 k
 libXpm                            x86_64           3.5.12-2.el7_9            ol7_latest            55 k
 libfontenc                        x86_64           1.1.3-3.el7               ol7_latest            30 k
 libpng                            x86_64           2:1.5.13-8.el7            ol7_latest           212 k
 libxkbfile                        x86_64           1.0.9-3.el7               ol7_latest            82 k

Transaction Summary
=========================================================================================================
Install  1 Package (+13 Dependent packages)

Total download size: 3.1 M
Installed size: 9.0 M
Downloading packages:
(1/14): dejavu-fonts-common-2.33-6.el7.noarch.rpm                                 |  64 kB  00:00:00
(2/14): fontconfig-2.13.0-4.3.el7.x86_64.rpm                                      | 254 kB  00:00:00
(3/14): fontpackages-filesystem-1.44-8.el7.noarch.rpm                             | 9.4 kB  00:00:00
(4/14): freetype-2.8-14.el7_9.1.x86_64.rpm                                        | 380 kB  00:00:00
(5/14): dejavu-sans-fonts-2.33-6.el7.noarch.rpm                                   | 1.4 MB  00:00:00
(6/14): libXcursor-1.1.15-1.el7.x86_64.rpm                                        |  30 kB  00:00:01
(7/14): libXfixes-5.0.3-1.el7.x86_64.rpm                                          |  18 kB  00:00:00
(8/14): libXaw-1.0.13-4.el7.x86_64.rpm                                            | 191 kB  00:00:01
(9/14): libXpm-3.5.12-2.el7_9.x86_64.rpm                                          |  55 kB  00:00:00
(10/14): libfontenc-1.1.3-3.el7.x86_64.rpm                                        |  30 kB  00:00:00
(11/14): libpng-1.5.13-8.el7.x86_64.rpm                                           | 212 kB  00:00:00
(12/14): libXft-2.3.2-2.el7.x86_64.rpm                                            |  58 kB  00:00:01
(13/14): libxkbfile-1.0.9-3.el7.x86_64.rpm                                        |  82 kB  00:00:01
(14/14): xorg-x11-apps-7.7-7.el7.x86_64.rpm                                       | 307 kB  00:00:01
---------------------------------------------------------------------------------------------------------
Total                                                                    555 kB/s | 3.1 MB  00:00:05
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : fontpackages-filesystem-1.44-8.el7.noarch                                            1/14
  Installing : 2:libpng-1.5.13-8.el7.x86_64                                                         2/14
  Installing : freetype-2.8-14.el7_9.1.x86_64                                                       3/14
  Installing : dejavu-fonts-common-2.33-6.el7.noarch                                                4/14
  Installing : dejavu-sans-fonts-2.33-6.el7.noarch                                                  5/14
  Installing : fontconfig-2.13.0-4.3.el7.x86_64                                                     6/14
  Installing : libXft-2.3.2-2.el7.x86_64                                                            7/14
  Installing : libfontenc-1.1.3-3.el7.x86_64                                                        8/14
  Installing : libXpm-3.5.12-2.el7_9.x86_64                                                         9/14
  Installing : libXaw-1.0.13-4.el7.x86_64                                                          10/14
  Installing : libXfixes-5.0.3-1.el7.x86_64                                                        11/14
  Installing : libXcursor-1.1.15-1.el7.x86_64                                                      12/14
  Installing : libxkbfile-1.0.9-3.el7.x86_64                                                       13/14
  Installing : xorg-x11-apps-7.7-7.el7.x86_64                                                      14/14
  Verifying  : fontconfig-2.13.0-4.3.el7.x86_64                                                     1/14
  Verifying  : libxkbfile-1.0.9-3.el7.x86_64                                                        2/14
  Verifying  : libXaw-1.0.13-4.el7.x86_64                                                           3/14
  Verifying  : libXfixes-5.0.3-1.el7.x86_64                                                         4/14
  Verifying  : dejavu-fonts-common-2.33-6.el7.noarch                                                5/14
  Verifying  : dejavu-sans-fonts-2.33-6.el7.noarch                                                  6/14
  Verifying  : libXcursor-1.1.15-1.el7.x86_64                                                       7/14
  Verifying  : 2:libpng-1.5.13-8.el7.x86_64                                                         8/14
  Verifying  : libXpm-3.5.12-2.el7_9.x86_64                                                         9/14
  Verifying  : libXft-2.3.2-2.el7.x86_64                                                           10/14
  Verifying  : libfontenc-1.1.3-3.el7.x86_64                                                       11/14
  Verifying  : freetype-2.8-14.el7_9.1.x86_64                                                      12/14
  Verifying  : fontpackages-filesystem-1.44-8.el7.noarch                                           13/14
  Verifying  : xorg-x11-apps-7.7-7.el7.x86_64                                                      14/14

Installed:
  xorg-x11-apps.x86_64 0:7.7-7.el7

Dependency Installed:
  dejavu-fonts-common.noarch 0:2.33-6.el7           dejavu-sans-fonts.noarch 0:2.33-6.el7
  fontconfig.x86_64 0:2.13.0-4.3.el7                fontpackages-filesystem.noarch 0:1.44-8.el7
  freetype.x86_64 0:2.8-14.el7_9.1                  libXaw.x86_64 0:1.0.13-4.el7
  libXcursor.x86_64 0:1.1.15-1.el7                  libXfixes.x86_64 0:5.0.3-1.el7
  libXft.x86_64 0:2.3.2-2.el7                       libXpm.x86_64 0:3.5.12-2.el7_9
  libfontenc.x86_64 0:1.1.3-3.el7                   libpng.x86_64 2:1.5.13-8.el7
  libxkbfile.x86_64 0:1.0.9-3.el7

Complete!
```

### 3. ip 設定
```sh
$ ipconfig

Windows IP Configuration

Ethernet adapter vEthernet (WSL):
   IPv4 Address. . . . . . . . . . . : 111.222.333.444

```

OSホストIPを oracle-database コンテナ `$DISPLAY` 環境変数に設定

```conf
DISPLAY=<host-ip>:<display-port>
```

```sh
bash-4.2# export DISPLAY=111.222.333.444:0.0
bash-4.2# echo $DISPLAY
111.222.333.444:0.0
```

`xeyes` を起動して挙動確認

```sh
bash-4.2# xeyes
```

![image](https://github.com/user-attachments/assets/979235d6-5a51-4487-8ae1-30a26236c278)
