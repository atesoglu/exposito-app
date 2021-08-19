# Get column name length distribution in SQL Server database

Query below returns distribution of column name lengths (number of characters).


``` sql
select len(col.name) as column_name_length,
       count(*) as columns,
       count(distinct tab.object_id) as tables
   from sys.tables as tab
       inner join sys.columns as col 
       on tab.object_id = col.object_id
group by len(col.name)
order by len(col.name)
```

ref: https://dataedo.com/kb/query/sql-server/column-name-length-distribution