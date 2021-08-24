# Find tables that are not used by any other object in SQL Server database

Query below lists all tables that are not referenced by any object .


``` sql
select schema_name(schema_id) as schema_name,
       name as table_name
from sys.tables tab
left join sys.sql_expression_dependencies dep
          on tab.object_id = dep.referenced_id
where dep.referenced_id is null
order by schema_name,
         table_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/find-tables-that-are-not-used-by-any-other-object