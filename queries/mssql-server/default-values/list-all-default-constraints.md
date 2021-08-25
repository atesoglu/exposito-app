# List all default constraints in SQL Server database

Query below lists default constraints defined in the database ordered by constraint name.


``` sql
select con.[name] as constraint_name,
    schema_name(t.schema_id) + '.' + t.[name]  as [table],
    col.[name] as column_name,
    con.[definition]
from sys.default_constraints con
    left outer join sys.objects t
        on con.parent_object_id = t.object_id
    left outer join sys.all_columns col
        on con.parent_column_id = col.column_id
        and con.parent_object_id = col.object_id
order by con.name
	
```

ref: https://dataedo.com/kb/query/sql-server/list-all-default-constraints-in-the-database