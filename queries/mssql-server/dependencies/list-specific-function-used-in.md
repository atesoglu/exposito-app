# Find where specific function is used in SQL Server database

Query below list objects where specific function is used.

``` sql
select schema_name(o.schema_id) + '.' + o.name as [function],
       'is used by' as ref,
       schema_name(ref_o.schema_id) + '.' + ref_o.name as [object],
       ref_o.type_desc as object_type
from sys.objects o
join sys.sql_expression_dependencies dep
     on o.object_id = dep.referenced_id
join sys.objects ref_o
     on dep.referencing_id = ref_o.object_id
where o.type in ('FN', 'TF', 'IF')
      and schema_name(o.schema_id) = 'dbo'  -- put schema name here
      and o.name = 'ufnLeadingZeros'  -- put function name here
order by [object];
	
```

ref: https://dataedo.com/kb/query/sql-server/find-where-specific-function-is-used