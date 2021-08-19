# List Views In Database

Query below lists all views in SQL Server database.

``` sql
select schema_name(schema_id) as schema_name,
       name as view_name
from sys.views
order by schema_name,
         view_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-views-in-a-database