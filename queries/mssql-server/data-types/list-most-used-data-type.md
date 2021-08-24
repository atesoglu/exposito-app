# Find most used data type in SQL Server database

Query below returns data types used in a database ordered by the number of their occurance.

``` sql
select t.name as data_type,
    count(*) as [columns],
    cast(100.0 * count(*) /
    (select count(*) from sys.tables as tab inner join
        sys.columns as col on tab.object_id = col.object_id)
            as numeric(36, 1)) as percent_columns,
      count(distinct tab.object_id) as [tables],
      cast(100.0 * count(distinct tab.object_id) /
      (select count(*) from sys.tables) as numeric(36, 1)) as percent_tables
  from sys.tables as tab
       inner join sys.columns as col
        on tab.object_id = col.object_id
       left join sys.types as t
        on col.user_type_id = t.user_type_id
group by t.name
order by count(*) desc
```

ref: https://dataedo.com/kb/query/sql-server/most-used-data-type-in-the-database