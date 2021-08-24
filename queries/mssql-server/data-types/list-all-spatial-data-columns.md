# Find all spatial data columns in SQL Server database

Spatial in SQL Server are columns with the following data types: geometry, geography

The query below lists all columns with spatial data types.


``` sql
select schema_name(t.schema_id) + '.' + t.name as [table],
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
where type_name(user_type_id) in ('geometry', 'geography')
order by [table],
         c.column_id;
```

ref: https://dataedo.com/kb/query/sql-server/find-all-spatial-columns