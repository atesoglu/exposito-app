# Check Server Version

Queries below return server version, edition and system information.

``` sql
SELECT CASE 
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '8.0%' THEN 'SQL Server 2000'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '9.0%' THEN 'SQL Server 2005'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '10.0%' THEN 'SQL Server 2008'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '10.5%' THEN 'SQL Server 2008 R2'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '11.0%' THEN 'SQL Server 2012'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '12.0%' THEN 'SQL Server 2014'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '13.0%' THEN 'SQL Server 2016'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '14.0%' THEN 'SQL Server 2017'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) >  '14.0.9' THEN 'Newer Than SQL Server 2017'
	ELSE 'Unknown' END AS [CommonName],
	SERVERPROPERTY('Edition') AS [Edition],
	@@VERSION AS [Version]
```
