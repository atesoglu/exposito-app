# Find tables that are not referenced by the foreign keys in SQL Server database

Query below lists tables that are not referenced by the foreign keys.


``` sql
select 'No FKs >-' foreign_keys,
    schema_name(fk_tab.schema_id) as schema_name,
    fk_tab.name as table_name
from sys.tables fk_tab
    left outer join sys.foreign_keys fk
        on fk_tab.object_id = fk.referenced_object_id
where fk.object_id is null
order by schema_name(fk_tab.schema_id),
    fk_tab.name
	
```

ref: https://dataedo.com/kb/query/sql-server/find-tables-that-are-not-referenced-by-the-foreign-keys