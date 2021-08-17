# List Tables In Database

Query below lists all tables in SQL Server database.

``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name,
       t.create_date,
       t.modify_date
from sys.tables t
order by schema_name,
         table_name;
```

ref: https://dataedo.com/kb/query/sql-server/list-of-tables-in-the-database