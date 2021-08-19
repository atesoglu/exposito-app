# Find tables with specific column name in SQL Server database

Query below finds all tables that have 'ProductID' column.


``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name
from sys.tables t
where t.object_id in 
    (select c.object_id 
      from sys.columns c
     where c.name = 'ProductID')
order by schema_name,
         table_name;
```

ref: https://dataedo.com/kb/query/sql-server/find-tables-with-specific-column-name