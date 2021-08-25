# Summary of default constraints in SQL Server database

Query below summarizes default constraints in a database listing all distinct default value definitions for columns with the number of their occurrence.


``` sql
select 
    con.[definition] as default_definition,
    count(distinct t.object_id) as [tables],
    count(col.column_id) as [columns]
from sys.objects t
    inner join sys.all_columns col
        on col.object_id = t.object_id
    left outer join sys.default_constraints con
        on con.parent_object_id = t.object_id
        and con.parent_column_id = col.column_id
where t.type = 'U'
group by con.[definition]
order by [columns] desc, [tables] desc
	
```

ref: https://dataedo.com/kb/query/sql-server/summary-of-default-constraints-in-a-database