# Find number of columns in SQL Server database

Query returns basic statistics of numbers of columns in a database.

``` sql
select [columns], 
    [tables], 
    CONVERT(DECIMAL(10,2),1.0*[columns]/[tables]) as average_column_count
from (
    select count(*) [columns],
           count(distinct schema_name(tab.schema_id) + tab.name) as [tables]
       from sys.tables as tab
            inner join sys.columns as col
                on tab.object_id = col.object_id
) q
```

ref: https://dataedo.com/kb/query/sql-server/find-number-of-columns-in-database