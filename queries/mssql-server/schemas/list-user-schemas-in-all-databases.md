# List User Schemas In All Databases

Query below list user created schemas in all databases.

``` sql
declare @query nvarchar(max)

set @query = 
(select 'select ''' + name + ''' as database_name,
              s.Name COLLATE DATABASE_DEFAULT as schema_name,
              u.name COLLATE DATABASE_DEFAULT as schema_owner 
        FROM ['+ name + '].sys.schemas s
        JOIN ['+ name + '].sys.sysusers u on u.uid = s.principal_id
        where u.issqluser = 1
              and u.name not in (''sys'', ''guest'', ''INFORMATION_SCHEMA'')
        union all '
    from sys.databases 
    where database_id > 4
    for xml path(''), type).value('.', 'nvarchar(max)')

set @query = left(@query,len(@query)-10) 
                        + ' order by database_name, schema_name'

execute (@query)
```

ref: https://dataedo.com/kb/query/sql-server/list-user-schemas-in-all-databases