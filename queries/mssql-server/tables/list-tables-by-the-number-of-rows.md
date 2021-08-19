# List tables by the number of rows in SQL Server database

This query returns list of tables in a database with their number of rows.


``` sql
select schema_name(tab.schema_id) + '.' + tab.name as [table], 
       sum(part.rows) as [rows]
   from sys.tables tab
        inner join sys.partitions part
            on tab.object_id = part.object_id
where part.index_id IN (1, 0) -- 0 - table without PK, 1 table with PK
group by schema_name(tab.schema_id) + '.' + tab.name
order by sum(part.rows) desc
```

ref: https://dataedo.com/kb/query/sql-server/list-of-tables-by-the-number-of-rows