# Find objects used by specific stored procedure in SQL Server database

Query below return all stored procedures and objects used by them.


``` sql
select schema_name(obj.schema_id) as schema_name,
       obj.name as procedure_name,
       schema_name(dep_obj.schema_id) as referenced_object_schema,
       dep_obj.name as referenced_object_name,
       dep_obj.type_desc as object_type
from sys.objects obj
left join sys.sql_expression_dependencies dep
          on dep.referencing_id = obj.object_id
left join sys.objects dep_obj
          on dep_obj.object_id = dep.referenced_id
where obj.type in ('P', 'X', 'PC', 'RF')
    --  and obj.name = 'procedure_name'  -- put procedure name here
order by schema_name,
         procedure_name;
	
```

ref: https://dataedo.com/kb/query/sql-server/find-objects-used-by-specific-stored-procedure