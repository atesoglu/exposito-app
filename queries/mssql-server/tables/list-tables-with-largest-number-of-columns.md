# List tables with the largest number of columns in SQL Server database

Query that returns tables with number of columns, ordered from the ones that have the most.


``` sql
select schema_name(tab.schema_id) + '.' + tab.name as [table], 
       count(*) as [columns]
   from sys.tables as tab
        inner join sys.columns as col
            on tab.object_id = col.object_id
group by schema_name(tab.schema_id), 
       tab.name
order by count(*) desc
```

ref: https://dataedo.com/kb/query/sql-server/list-of-tables-with-the-most-columns