# Compare tables and columns in two databases on SQL Server

Query below compares columns (names) in tables between two SQL Server databases. It shows columns missing in either of two databases.


``` sql
select isnull(db1.table_name, db2.table_name) as [table],
       isnull(db1.column_name, db2.column_name) as [column],
       db1.column_name as database1, 
       db2.column_name as database2
from
(select schema_name(tab.schema_id) + '.' + tab.name as table_name, 
       col.name as column_name
   from database1.sys.tables as tab
        inner join database1.sys.columns as col
            on tab.object_id = col.object_id) db1
full outer join
(select schema_name(tab.schema_id) + '.' + tab.name as table_name, 
       col.name as column_name
   from database2.sys.tables as tab
        inner join database2.sys.columns as col
            on tab.object_id = col.object_id) db2
on db1.table_name = db2.table_name
and db1.column_name = db2.column_name
where (db1.column_name is null or db2.column_name is null)
order by 1, 2, 3
```

ref: https://dataedo.com/kb/query/sql-server/compare-tables-and-columns-in-two-databases