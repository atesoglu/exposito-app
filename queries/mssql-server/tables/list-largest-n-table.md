# List N largest tables in SQL Server

Query below list largest N tables in database.


``` sql
select top 10 schema_name(tab.schema_id) + '.' + tab.name as [table], 
    cast(sum(spc.used_pages * 8)/1024.00 as numeric(36, 2)) as used_mb,
    cast(sum(spc.total_pages * 8)/1024.00 as numeric(36, 2)) as allocated_mb
from sys.tables tab
join sys.indexes ind 
     on tab.object_id = ind.object_id
join sys.partitions part 
     on ind.object_id = part.object_id and ind.index_id = part.index_id
join sys.allocation_units spc
     on part.partition_id = spc.container_id
group by schema_name(tab.schema_id) + '.' + tab.name
order by sum(spc.used_pages) desc;
```

ref: https://dataedo.com/kb/query/sql-server/list-10-largest-tables