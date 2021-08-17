# List Temporal Tables

```
This query works on SQL Server 2017 or newer.
```
SQL Server 2016 and 2017 brought new features and table types - temporal tables (2016), external tables (2016) and graph tables (2017).

Query below lists tables in current database and identifies it's type. Types include:

Plan old Regular table
Graph node table (introduced in SQL Server 2017)
Graph edge table (introduced in SQL Server 2017)
System versioned table (temporal table) (introduced in SQL Server 2016)
History table (introduced in SQL Server 2016)
PolyBase External table (introduced in SQL Server 2016)
File table (introduced in SQL Server 2012)

``` sql
select schema_name(schema_id) as schema_name,
       name as table_name,
        case when is_external = 1 then 'External table'
            when is_node = 1 then 'Graph node table'
            when is_edge = 1 then 'Graph edge table'
            when temporal_type = 2 then 'System versioned table'
            when temporal_type = 1 then 'History table'
            when is_filetable = 1 then 'File table'
            else 'Regular table'
        end as table_type
        from sys.tables
order by schema_name, table_name
```

ref: https://dataedo.com/kb/query/sql-server/identify-table-types-in-sql-server-2017