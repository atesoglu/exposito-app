# Find tables with digits in names in SQL Server database

Tables usually do not have digits in their names, and if they do they have a special meaning. We use them to name backup tables with date of an backup (of single specific table while sensitive operation), archival tables with year or for partitioning tables.


``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name
from sys.tables t
where t.name like '%[0-9]%'
order by schema_name,
         table_name;
```

ref: https://dataedo.com/kb/query/sql-server/find-tables-with-digits-in-names