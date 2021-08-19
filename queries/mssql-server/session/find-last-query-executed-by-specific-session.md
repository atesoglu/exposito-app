# Find last query executed by specific session on SQL Server

SQL Server enables you to check last query executed by each session. Queries in this article will show you how to do it.


## Find a session

First you need to identify session. Find out more here:


``` sql
exec sp_who
	
```

## Find last query

Now we will use session ID (spid) to find last query issued in this session:


``` sql
dbcc inputbuffer(<session ID>)
	
```

EventType - event type. RPC Event means procedure call. Language Event means sql query.
Parameters - number of query parameters.
EventInfo - last statement in session. Returns only first 4000 characters

ref: https://dataedo.com/kb/query/sql-server/find-last-query-executed-by-session