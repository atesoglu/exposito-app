# Tables don't have primary keys (with percentage) in SQL Server database

This query listed tables without primary keys and this one shows how many of them there are and what is the percentage of total tables.


``` sql
select 
    all_tabs.[tables] as all_tables,
    no_pk.[tables] as no_pk_tables,
    cast(cast(100.0 * no_pk.[tables] / 
    all_tabs.[tables] as decimal(36, 1)) as varchar) + '%' as no_pk_percent
from
    (select count(*) as [tables]
    from sys.tables tab
        left outer join sys.indexes pk
            on tab.object_id = pk.object_id 
            and pk.is_primary_key = 1
    where pk.object_id is null) as no_pk
inner join 
    (select count(*) as [tables]
    from sys.tables) as all_tabs
on 1 = 1
	
```

ref: https://dataedo.com/kb/query/sql-server/how-many-tables-dont-have-primary-keys