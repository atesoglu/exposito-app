# List Databases

Query below lists databases on SQL Server instance.

``` sql
SELECT schema_name(t.schema_id) AS SchemaName, t.name AS TableName, col.column_id AS ColumnId, col.name AS ColumnName, tt.name as DataType, col.max_length AS [MaxLength], col.[precision] AS [Precision]
FROM sys.tables t
	INNER JOIN sys.columns col ON t.object_id = col.object_id
	LEFT JOIN sys.types as tt ON col.user_type_id = tt.user_type_id
ORDER BY schema_name(t.schema_id), TableName, ColumnId;
```

ref: https://dataedo.com/kb/query/sql-server/list-databases