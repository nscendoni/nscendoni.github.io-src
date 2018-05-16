Title: Flashback Configuration
Category: Oracle
Date: 2017-04-04

###Enable Flashback
```
sqlplus '/ as sysdba'
ALTER DATABASE ARCHIVELOG
```
_restart_
```
alter system set db_recovery_file_dest='/opt/dbs/oracle/MDR/flash' 
alter system set db_recovery_file_dest_size=100G
shutdown immediate;
startup mount;
alter database flashback on;
-- retention here is 48 hours (values in minutes)
alter system set db_flashback_retention_target=2880;
```
_restart_

##How to revert the database to a specific SCN Number or date

### GET SCN Number:
```
Execute one of the below:
select TO_CHAR(systimestamp) from dual;
select systimestamp from dual;
```

### Flashback from SCN Number
```
sqlplus / as sysdba
SHUTDOWN IMMEDIATE;
STARTUP MOUNT
```
Execute one of the below:
```
FLASHBACK DATABASE TO SCN 13735378177502;
FLASHBACK database TO TIMESTAMP TO_TIMESTAMP('2014-01-15 12:00:00', 'YYYY-MM-DD HH24:MI:SS');
alter database open resetlogs;
```

### Create Restore Point
```
sqlplus '/ as sysdba'
create restore point first_restore_point;
```
### List Restore Point
```
sqlplus '/ as sysdba'
select name, time from v$restore_point;
```
### Restore Flashback
```
stop database

sqlplus '/ as sysdba'
startup mount;
flashback database to restore point first_restore_point;
alter database open resetlogs;
start database
```


