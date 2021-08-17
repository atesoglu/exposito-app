# List Temporal Tables

```
This query works on SQL Server 2016 or newer.
```

SQL Server 2016 brought exciting and useful feature - system-versioned temporal tables that implement change tracking managed by server itself. Server manages 2 separate tables - system-versioned temporal table with actual data and history table that stores change history.

Query below returns temporal tables paired with their history tables and retention period (how long history is stored).


``` sql
select schema_name(t.schema_id) as temporal_table_schema,
     t.name as temporal_table_name,
    schema_name(h.schema_id) as history_table_schema,
     h.name as history_table_name,
    case when t.history_retention_period = -1 
        then 'INFINITE' 
        else cast(t.history_retention_period as varchar) + ' ' + 
            t.history_retention_period_unit_desc + 'S'
    end as retention_period
from sys.tables t
    left outer join sys.tables h
        on t.history_table_id = h.object_id
where t.temporal_type = 2
order by temporal_table_schema, temporal_table_name
```

ref: https://dataedo.com/kb/query/sql-server/list-temporal-tables-in-database