# Find table that DON'T have a column with specific name in SQL Server database

Databases often have standard columns. Examples of such standard columns can be id, modified_date, created_by or row_version.


``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name
from sys.tables t
where t.object_id not in 
    (select c.object_id 
      from sys.columns c
     where c.name = 'ModifiedDate')
order by schema_name,
         table_name;
```

ref: https://dataedo.com/kb/query/sql-server/find-table-that-dont-have-a-column-with-specific-name