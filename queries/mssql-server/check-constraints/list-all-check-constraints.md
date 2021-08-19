# List all check constraints in SQL Server database

Query below lists check constraints defined in the database ordered by constraint name.


``` sql
select con.[name] as constraint_name,
    schema_name(t.schema_id) + '.' + t.[name]  as [table],
    col.[name] as column_name,
    con.[definition],
    case when con.is_disabled = 0 
        then 'Active' 
        else 'Disabled' 
        end as [status]
from sys.check_constraints con
    left outer join sys.objects t
        on con.parent_object_id = t.object_id
    left outer join sys.all_columns col
        on con.parent_column_id = col.column_id
        and con.parent_object_id = col.object_id
order by con.name
	
```

ref: https://dataedo.com/kb/query/sql-server/list-check-constraints-in-database