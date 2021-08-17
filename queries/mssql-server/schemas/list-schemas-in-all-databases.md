# List Schemas In All Databases

Query below lists all schemas from all databases on SQL Server instance.

``` sql
declare @query nvarchar(max);

set @query =
(select 'select ''' + name + ''' as database_name,
                name COLLATE DATABASE_DEFAULT as schema_name 
         from ['+ name + '].sys.schemas union all '
  from sys.databases 
  where database_id > 4
  for xml path(''), type).value('.', 'nvarchar(max)');

set @query = left(@query,len(@query)-10) + ' order by database_name, schema_name';
execute (@query);
```

ref: https://dataedo.com/kb/query/sql-server/list-schemas-in-all-databases