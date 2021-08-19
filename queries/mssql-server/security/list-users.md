# List users in SQL Server database

Query below returns list of users in current database.


``` sql
select name as username,
       create_date,
       modify_date,
       type_desc as type,
       authentication_type_desc as authentication_type
from sys.database_principals
where type not in ('A', 'G', 'R', 'X')
      and sid is not null
      and name != 'guest'
order by username;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-users-in-database