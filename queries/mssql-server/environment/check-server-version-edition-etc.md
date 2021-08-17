# Check Server Version

Queries below return server version, edition and system information.

``` sql
SELECT 
	
	CASE 
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '8.0%' THEN 'SQL Server 2000'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '9.0%' THEN 'SQL Server 2005'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '10.0%' THEN 'SQL Server 2008'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '10.5%' THEN 'SQL Server 2008 R2'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '11.0%' THEN 'SQL Server 2012'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '12.0%' THEN 'SQL Server 2014'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '13.0%' THEN 'SQL Server 2016'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '14.0%' THEN 'SQL Server 2017'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) LIKE '15.0%' THEN 'SQL Server 2019'
		WHEN CONVERT(SYSNAME, SERVERPROPERTY('ProductVersion')) >  '15.0.9' THEN 'Newer Than SQL Server 2019'
		ELSE 'Unknown' 
	END AS [ProductVersion],

	SERVERPROPERTY('Edition') AS [Edition],

	CASE WHEN SERVERPROPERTY('EngineEdition') = 1 THEN 'Personal/Desktop'
        WHEN SERVERPROPERTY('EngineEdition') = 2 THEN 'Standard'
        WHEN SERVERPROPERTY('EngineEdition') = 3 THEN 'Enterprise'
        WHEN SERVERPROPERTY('EngineEdition') = 4 THEN 'Express'
        WHEN SERVERPROPERTY('EngineEdition') = 5 THEN 'SQL Database'
        WHEN SERVERPROPERTY('EngineEdition') = 6 THEN 'SQL Data Warehouse'
        WHEN SERVERPROPERTY('EngineEdition') = 8 THEN 'Managed Instance'
    END AS [EngineEdition],

	@@VERSION AS [Version],

	host_platform AS HostPlatform, host_distribution AS HostDistribution, host_release AS HostRelease

FROM sys.dm_os_host_info;
	
```

ref: https://dataedo.com/kb/query/sql-server/check-server-version
ref: https://dataedo.com/kb/query/sql-server/check-server-edition
ref: https://dataedo.com/kb/query/sql-server/how-to-find-operating-system-os-that-server-runs-on