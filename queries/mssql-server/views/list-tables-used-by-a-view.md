# List Tables Used By A View

Query below lists views in a database with their references.

```
Notes: This query doesn't include cross database references. This query lists only references within database.
```


``` sql
select distinct schema_name(v.schema_id) as schema_name,
       v.name as view_name,
       schema_name(o.schema_id) as referenced_schema_name,
       o.name as referenced_entity_name,
       o.type_desc as entity_type
from sys.views v
join sys.sql_expression_dependencies d
     on d.referencing_id = v.object_id
     and d.referenced_id is not null
join sys.objects o
     on o.object_id = d.referenced_id
 order by schema_name,
          view_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-tables-used-by-a-view