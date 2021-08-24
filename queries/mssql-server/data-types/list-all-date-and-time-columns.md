# Find all date and time columns in SQL Server database

Date and time in SQL Server are represented by following data types: date, time, datetime, datetime2, smalldatetime, datetimeoffset, . The query below lists all columns with date/time data types.


``` sql
select schema_name(t.schema_id) + '.' + t.name as [table],
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       scale as second_scale
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
where type_name(user_type_id) in ('date', 'datetimeoffset', 
      'datetime2', 'smalldatetime', 'datetime', 'time')
order by [table],
         c.column_id;
```

ref: https://dataedo.com/kb/query/sql-server/find-all-date-and-time-columns