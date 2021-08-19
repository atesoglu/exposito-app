# List Views With Scripts In Database

Query below lists views in a database with their definition.

``` sql
select schema_name(v.schema_id) as schema_name,
       v.name as view_name,
       v.create_date as created,
       v.modify_date as last_modified,
       m.definition
from sys.views v
join sys.sql_modules m 
     on m.object_id = v.object_id
 order by schema_name,
          view_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-views-with-their-scripts