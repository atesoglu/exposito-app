# List idexes by their size in SQL Server

Query below returns list indexes and their size.


``` sql
select ind.name as [index_name],
    ind.type_desc as index_type,
    cast(sum(spc.used_pages * 8)/1024.00 as numeric(36,2)) as used_mb,
    cast(sum(spc.total_pages * 8)/1024.00 as numeric(36,2)) as allocated_mb,
    cast(sum(spc.data_pages * 8)/1024.00 as numeric(36,2)) as data_space_mb,
    ind.is_unique,
    ind.is_primary_key,
    ind.is_unique_constraint,
    schema_name(obj.schema_id) + '.' + obj.name as object_name,
    obj.type_desc as type
from sys.indexes ind
join sys.objects obj 
        on obj.object_id = ind.object_id
        and obj.type in ('U','V')
join sys.partitions part 
        on ind.object_id = part.object_id 
        and ind.index_id = part.index_id
join sys.allocation_units spc
     on part.partition_id = spc.container_id
where ind.index_id > 0
group by obj.schema_id, obj.name, ind.name, ind.type_desc, 
         ind.is_unique, ind.is_primary_key, ind.is_unique_constraint, 
         obj.type_desc
order by sum(spc.total_pages) desc;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-of-idexes-by-their-size