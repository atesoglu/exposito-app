# Find all string and binary columns in SQL Server database

In SQL Server string and binary columns are with the following data types: text, ntext, varchar, nvarchar, char, nchar, binary, varbinary, image.

The query below lists all columns with string and binary data types.


``` sql
select schema_name(t.schema_id) + '.' + t.name as [table],
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       max_length 
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
where type_name(user_type_id) in ('text', 'ntext',
      'varchar', 'nvarchar', 'char', 'nchar',
      'binary', 'varbinary', 'image')
order by [table],
         c.column_id;
```

ref: https://dataedo.com/kb/query/sql-server/find-all-string-columns