# Find large object (LOB) data type columns in SQL Server database

Large objects in SQL Server are columns with following data types: varchar(max), nvarchar(max), text, ntext, image, varbinary(max), and xml.

Query below lists all columns with LOB data types.


``` sql
select t.table_schema as schema_name,
    t.table_name, 
    c.column_name,
    c.data_type
from information_schema.columns c
    inner join information_schema.tables t
        on c.table_schema = t.table_schema
        and c.table_name = t.table_name
where t.table_type = 'BASE TABLE' 
and ((c.data_type in ('VARCHAR', 'NVARCHAR') and character_maximum_length = -1)
or c.data_type in ('TEXT', 'NTEXT', 'IMAGE', 'VARBINARY', 'XML', 'FILESTREAM'))
order by t.table_schema, 
    t.table_name,
    c.column_name
```

ref: https://dataedo.com/kb/query/sql-server/find-large-object-lob-data-type-columns