# Find all numeric columns in SQL Server database

Numeric in SQL Server are columns with the following data types: tinyint, smallint, int, bigint, decimal, numeric, bit, float, real, smallmoney and money. The query below lists all columns with numeric data types.


``` sql
select schema_name(t.schema_id) + '.' + t.name as [table],
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       max_length,
       precision,
       scale 
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
where type_name(user_type_id) in ('bigint', 'int', 
      'smallint', 'tinyint', 'decimal', 'numeric',
      'smallmoney', 'money', 'bit', 'float', 'real')
order by [table],
         c.column_id;
```

ref: https://dataedo.com/kb/query/sql-server/find-all-numeric-columns