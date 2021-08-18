# Check if is column nullable in SQL Server database

Query below check nullability attribute for the column.


``` sql
select schema_name(t.schema_id) as schema_name,
       t.name as table_name,
       c.name as column_name,
       case is_nullable
            when 0 then 'NOT NULLABLE'
            else 'NULLABLE'
            end as nullable
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
order by schema_name,
         table_name,
         column_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/check-column-nullable