# Find a table by the name in SQL Server database

Query below finds tables with specific name in all schemas in a database. In this case it searches for 'customer' table.


``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name
from sys.tables t
where t.name = 'customer'
order by schema_name,
         table_name;
```

ref: https://dataedo.com/kb/query/sql-server/find-a-table-by-the-name