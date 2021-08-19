# Find most popular column names in SQL Server database

This query lets you find out most popular column names.


``` sql
select col.name as column_name,
      count(*) as tables,
      cast(100.0 * count(*) / 
      (select count(*) from sys.tables) as numeric(36, 1)) as percent_tables
   from sys.tables as tab
       inner join sys.columns as col 
       on tab.object_id = col.object_id
group by col.name 
having count(*) > 1
order by count(*) desc
```

ref: https://dataedo.com/kb/query/sql-server/most-popular-column-names