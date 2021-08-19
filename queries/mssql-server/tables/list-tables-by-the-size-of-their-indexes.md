# List tables by the size of their indexes in SQL Server

Query below returns tables in a database with space used by their indexes ordered from the ones using most.


``` sql
select schema_name(tab.schema_id) + '.' + tab.name as [table],
       (sum(spc.total_pages * 8) / 1024.0) as allocated_space,
       (sum(spc.used_pages * 8) / 1024.0) as used_space
from sys.tables tab
join sys.indexes ind
     on tab.object_id = ind.object_id
join sys.partitions part
     on ind.object_id = part.object_id
     and ind.index_id = part.index_id
join sys.allocation_units spc
     on part.partition_id = spc.container_id
group by tab.schema_id, tab.name
order by used_space desc;
```

ref: https://dataedo.com/kb/query/sql-server/list-of-tables-by-the-size-of-their-indexes