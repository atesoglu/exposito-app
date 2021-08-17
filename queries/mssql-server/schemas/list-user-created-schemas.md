# List User Created Schemas

Query below lists user schemas in SQL Server database, excluding default db_* , sys, information_schema and guest schemas.
If you want to list all schemas use 'List Schemas'.

``` sql
select s.name as schema_name, 
    s.schema_id,
    u.name as schema_owner
from sys.schemas s
    inner join sys.sysusers u
        on u.uid = s.principal_id
where u.issqluser = 1
    and u.name not in ('sys', 'guest', 'INFORMATION_SCHEMA')
```

ref: https://dataedo.com/kb/query/sql-server/list-user-schemas-in-database