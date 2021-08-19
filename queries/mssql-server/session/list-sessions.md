# List sessions / active connections in SQL Server

There are two procedures useful in debugging session problems.
PS: Please note that you need VIEW SERVER STATE permission to view all the sessions. Otherwise you'll only see yor own.


## Official command

``` sql
exec sp_who
	
```

spid - unique session ID
status - process status
loginname - login name associated with the session. You can use ti to identify application user
hostname - host name associated with the session. You can use ti to identify application user
blk - session ID of the blocking process (spid is blocked by blk)
dbname - database used by process

## More verbose command

SQL Server has also second version of this procedure - sp_who2. This procedure shows some more information that you can use to identify process.


``` sql
exec sp_who2
	
```

all columns from sp_who, plus:
ProgramName - application associated with the session Many applications set this useful value
LastBatch - last activity associated with the session


ref: https://dataedo.com/kb/query/sql-server/list-database-sessions