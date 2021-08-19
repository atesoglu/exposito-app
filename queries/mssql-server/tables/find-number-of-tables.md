# Find number of tables in SQL Server database

Query below returns total number of tables in current database.


``` sql
select count(*) as [tables]
   from sys.tables 
```

ref: https://dataedo.com/kb/query/sql-server/find-number-of-tables-in-database