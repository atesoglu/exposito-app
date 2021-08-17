# List Tables In Schema

Query below lists all tables in specific schema in SQL Server database.

``` sql
SELECT SCHEMA_NAME(t.SCHEMA_ID) AS SchemaName, t.name AS TableName, t.create_date AS CreatedAt, t.modify_date AS ModifiedAt
FROM sys.tables t
WHERE SCHEMA_NAME(t.SCHEMA_ID) = 'dbo'
ORDER BY t.name;
```

ref: https://dataedo.com/kb/query/sql-server/list-of-tables-in-schema