# Find tables not accessed for past n months in SQL Server database

Query below returns list of tables that was not accessed in the last 3 month.

Note: 
In SQL Server you can find out when table was last accessed by quering dm_db_index_usage_stats view, but note that this view is cleaned each time SQL Server is restarted.

``` sql
select [schema_name],
       table_name,
       max(last_access) as last_access
from(
    select schema_name(schema_id) as schema_name,
           name as table_name,
           (select max(last_access) 
            from (values(last_user_seek),
                        (last_user_scan),
                        (last_user_lookup), 
                        (last_user_update)) as tmp(last_access))
                as last_access
from sys.dm_db_index_usage_stats sta
join sys.objects obj
     on obj.object_id = sta.object_id
     and obj.type = 'U'
     and sta.database_id = DB_ID()
) usage
where last_access < dateadd(month, -3, current_timestamp)
group by schema_name,
         table_name
order by last_access desc;
```

ref: https://dataedo.com/kb/query/sql-server/find-empty-tables-in-database