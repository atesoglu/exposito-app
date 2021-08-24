# List most referenced tables (by FK) in SQL Server database

Query below lists tables that are most referenced by other tables with foreign keys. Those are the dictionary tables such as person, product or store. In data warehouses those are dimension tables.


``` sql
select schema_name(tab.schema_id) + '.' + tab.name as [table],
   count(fk.name) as [references],
   count(distinct fk.parent_object_id) as referencing_tables
from sys.tables as tab
   left join sys.foreign_keys as fk
       on tab.object_id = fk.referenced_object_id
group by schema_name(tab.schema_id), tab.name
having count(fk.name) > 0
order by 2 desc
	
```

ref: https://dataedo.com/kb/query/sql-server/list-most-referenced-tables-in-a-database