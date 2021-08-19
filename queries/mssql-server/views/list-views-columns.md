# List Views Columns

Query below lists all columns in views in SQL Server database.

``` sql
select schema_name(v.schema_id) as schema_name,
       object_name(c.object_id) as view_name,
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       c.max_length,
       c.precision
from sys.columns c
join sys.views v 
     on v.object_id = c.object_id
order by schema_name,
         view_name,
         column_id;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-views-columns