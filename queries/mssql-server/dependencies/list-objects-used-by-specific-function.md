# Find objects used by specific function in SQL Server database

Query below return all User Defined Functions and objects used by them.

``` sql
select schema_name(obj.schema_id) as schema_name,
       obj.name as function_name,
       schema_name(dep_obj.schema_id) as referenced_object_schema,
       dep_obj.name as referenced_object_name,
       dep_obj.type_desc as object_type
FROM sys.objects obj
left join sys.sql_expression_dependencies dep
     on dep.referencing_id = obj.object_id
left join sys.objects dep_obj
     on dep_obj.object_id = dep.referenced_id
where obj.type in ('AF', 'FN', 'FS', 'FT', 'IF', 'TF')
     -- and obj.name = 'function_name'  -- put function name here
order by schema_name,
         function_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/find-objects-used-by-specific-function