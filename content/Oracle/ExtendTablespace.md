Title: Extend tablespace
Category: Oracle
Date: 2012-02-03 00:12

```
sqlplus / as sysdba
select * from v$tablespace;

SELECT dd.tablespace_name tablespace_name, dd.file_name file_name, dd.bytes/1024 TABLESPACE_KB, SUM(fs.bytes)/1024 KBYTES_FREE, MAX(fs.bytes)/1024 NEXT_FREE
FROM sys.dba_free_space fs, sys.dba_data_files dd
WHERE dd.tablespace_name = fs.tablespace_name
AND dd.file_id = fs.file_id
GROUP BY dd.tablespace_name, dd.file_name, dd.bytes/1024
ORDER BY dd.tablespace_name, dd.file_name;


ALTER TABLESPACE mds_data
   ADD DATAFILE '/dbs/oracle/MDR/mds1.dbf' SIZE 1G;
```

