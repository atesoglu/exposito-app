# Loner Ratio - how many tables have no relationships in SQL Server database

This query listed tables that have no foreign keys, meaning they are not referencing any table or are not on the "many" side of FK.

Query below lists something a little different - tables that are not referencing and are not referenced by other tables. Something I called Loner Tables.


``` sql
select count(*) [table_count],
    sum(case when fks.cnt + refs.cnt = 0 then 1 else 0 end) 
    as [loner_tables],
    cast(cast(100.0 * sum(case when fks.cnt + refs.cnt = 0 then 1 else 0 end) 
    / count(*) as decimal(36, 1)) as varchar) + '%' as [loner_ratio]
from (select schema_name(tab.schema_id) + '.' + tab.name as tab,
        count(fk.name) cnt
    from sys.tables as tab
        left join sys.foreign_keys as fk
            on tab.object_id = fk.parent_object_id
    group by schema_name(tab.schema_id), tab.name) fks
    inner join 
    (select schema_name(tab.schema_id) + '.' + tab.name as tab,
        count(fk.name) cnt
    from sys.tables as tab
        left join sys.foreign_keys as fk
            on tab.object_id = fk.referenced_object_id
    group by schema_name(tab.schema_id), tab.name) refs
    on fks.tab = refs.tab
	
```

ref: https://dataedo.com/kb/query/sql-server/loner-ratio-how-many-tables-have-no-relationships