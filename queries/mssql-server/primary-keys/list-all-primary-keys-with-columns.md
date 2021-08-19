# List all primary keys (PKs) and their columns in SQL Server database

Query below lists all primary keys constraints (PK) in the database with their columns (one row per column).


``` sql
select schema_name(tab.schema_id) as [schema_name], 
    pk.[name] as pk_name,
    ic.index_column_id as column_id,
    col.[name] as column_name, 
    tab.[name] as table_name
from sys.tables tab
    inner join sys.indexes pk
        on tab.object_id = pk.object_id 
        and pk.is_primary_key = 1
    inner join sys.index_columns ic
        on ic.object_id = pk.object_id
        and ic.index_id = pk.index_id
    inner join sys.columns col
        on pk.object_id = col.object_id
        and col.column_id = ic.column_id
order by schema_name(tab.schema_id),
    pk.[name],
    ic.index_column_id
	
```

ref: https://dataedo.com/kb/query/sql-server/list-all-primary-keys-and-their-columns