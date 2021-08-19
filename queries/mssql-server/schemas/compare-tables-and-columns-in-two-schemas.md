# Compare tables and columns in two schemas in SQL Server schemas

Query below compares columns (names) in tables between two SQL Server schemas. It shows columns missing in either of two schemas.

``` sql
select isnull(schema1.table_name, schema2.table_name) as [table],
       isnull(schema1.column_name, schema2.column_name) as [column],
       schema1.column_name as database1,
       schema2.column_name as database2
from
(select tab.name as table_name, 
        col.name as column_name
 from sys.tables as tab
 join sys.columns as col
      on tab.object_id = col.object_id
 where schema_name(tab.schema_id) = 'schema_1') schema1
full join
(select tab.name as table_name, 
        col.name as column_name
 from sys.tables as tab
 join sys.columns as col
      on tab.object_id = col.object_id
 where schema_name(tab.schema_id) = 'schema_2') schema2
on schema1.table_name = schema2.table_name
and schema1.column_name = schema2.column_name
where (schema1.column_name is null or schema2.column_name is null)
order by 1, 2, 3
```

ref: https://dataedo.com/kb/query/sql-server/compare-tables-and-columns-in-two-schemas