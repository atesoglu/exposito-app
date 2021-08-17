# Recently Created Tables In Database

Query below lists all tables in SQL Server database that were created within the last 30 days

``` sql
select schema_name(schema_id) as schema_name, name as table_name, create_date, modify_date
from sys.tables
where create_date > DATEADD(DAY, -30, CURRENT_TIMESTAMP)
order by create_date desc;
```

ref: https://dataedo.com/kb/query/sql-server/find-recently-created-tables