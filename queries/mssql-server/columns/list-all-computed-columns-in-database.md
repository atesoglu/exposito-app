# List All Computed Columns In Database

Query below lists all computed columns in SQL Server database.

``` sql
select schema_name(o.schema_id) as schema_name,
       object_name(c.object_id) as table_name,
       column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       definition
from sys.computed_columns c
join sys.objects o on o.object_id = c.object_id
order by schema_name,
         table_name,
         column_id;
```

ref: https://dataedo.com/kb/query/sql-server/list-all-computed-columns-in-the-database