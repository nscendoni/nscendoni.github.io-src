Title: Configuring Oracle DB for EUS Authentication
Category: Oracle
Date: 2015-12-3 22:00

1. Install OUD with support for EUS
Set Env variables and register the database:
```
[oracle@rhel62 ~]$ export ORACLE_HOME=/opt/oracle/product/ora/11.2.0
[oracle@rhel62 ~]$ export PATH=$PATH:/opt/oracle/product/ora/11.2.0/bin
```
2. Run `netca`. Both LDAP and LDAPS ports must be specified. Anonymous bind must be enabled. 
3. Run `dbca`. Specify the password for the Bind User and the password for the wall that will store that password.
4. Check that:

`ldap.ora` file is created
`sqlnet.ora` file is created

5. Create global user on Database and give some privileges:

```
[oracle@rhel62 bin]$ sqlplus / as sysdba

SQL*Plus: Release 11.2.0.3.0 Production on Tue Mar 24 11:48:22 2015

Copyright (c) 1982, 2011, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Enterprise Edition Release 11.2.0.3.0 - 64bit Production
With the Partitioning, OLAP, Data Mining and Real Application Testing options

SQL> create user test1 identified globally;

User created.

SQL> grant create session to test1;

Grant succeeded.

SQL> grant connect to test1;

Grant succeeded.


SQL> quit
```
5. Create the mapping:
```
[oracle@rhel62 ~]$ eusm createMapping domain_name=OracleDefaultDomain \
realm_dn=dc=nscendoni,dc=net ldap_host=localhost ldap_port=3389 \
ldap_user_dn="cn=Directory Manager" ldap_user_password="Welcome1" \
map_type="ENTRY" map_dn="uid=scendni1,ou=People,dc=nscendoni,dc=net" \
schema="test1"
```
