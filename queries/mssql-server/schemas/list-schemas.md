# List schemas in SQL Server database

Query below lists all schemas in SQL Server database. Schemas include default db_* , sys, information_schema and guest schemas.
If you want to list user only schemas use 'List user created schemas'.

``` sql
select s.name as schema_name, 
    s.schema_id,
    u.name as schema_owner
from sys.schemas s
    inner join sys.sysusers u
        on u.uid = s.principal_id
order by s.name
```

ref: https://dataedo.com/kb/query/sql-server/list-schemas-in-database