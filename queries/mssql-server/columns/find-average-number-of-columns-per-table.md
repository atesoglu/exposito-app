# Average number of columns per table in SQL Server database

Query below returns the average number of columns per table in a database.


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

ref: https://dataedo.com/kb/query/sql-server/average-number-of-columns