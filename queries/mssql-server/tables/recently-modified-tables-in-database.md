# Recently Modified Tables In Database

The query below lists all tables that was modified in the last 30 days by ALTER statement.

``` sql
select schema_name(schema_id) as schema_name, name as table_name, create_date, modify_date
from sys.tables
where modify_date > DATEADD(DAY, -30, CURRENT_TIMESTAMP)
order by modify_date desc;
```

ref: https://dataedo.com/kb/query/sql-server/find-recently-modified-tables