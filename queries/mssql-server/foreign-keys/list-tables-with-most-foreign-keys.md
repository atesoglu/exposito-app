# List tables with most foreign keys in SQL Server database

Query below lists tables with their number of foreign keys and number of tables they refer to.


``` sql
select schema_name(fk_tab.schema_id) + '.' + fk_tab.name as [table],
    count(*) foreign_keys,
    count (distinct referenced_object_id) referenced_tables
from sys.foreign_keys fk
    inner join sys.tables fk_tab
        on fk_tab.object_id = fk.parent_object_id
group by schema_name(fk_tab.schema_id) + '.' + fk_tab.name
order by count(*) desc
	
```

ref: https://dataedo.com/kb/query/sql-server/list-tables-with-most-foreign-keys