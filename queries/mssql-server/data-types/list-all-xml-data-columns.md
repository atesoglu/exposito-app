# Find all XML data columns in SQL Server database

The query below lists all columns with XML data types in SQL Server database.


``` sql
select schema_name(t.schema_id) + '.' + t.name as [table],
       c.column_id,
       c.name as column_name,
       type_name(user_type_id) as data_type,
       is_xml_document
       /*
       1 - content is a complete XML document with only one root element
       0 - content is a document fragment*/
       
from sys.columns c
join sys.tables t
     on t.object_id = c.object_id
where type_name(user_type_id) in ('xml')
order by [table],
         c.column_id;
```

ref: https://dataedo.com/kb/query/sql-server/find-all-xml-columns