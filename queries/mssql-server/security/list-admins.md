# List admins on SQL Server

Query below returns list of logins in current SQL Server instance with admin privileges.


``` sql
select mp.name as login,
       case when mp.is_disabled = 1 then 'Disabled'
            else 'Enabled'
            end as status,
      mp.type_desc as type
from sys.server_role_members srp 
join sys.server_principals mp 
     on mp.principal_id = srp.member_principal_id
join sys.server_principals rp 
     on rp.principal_id = srp.role_principal_id
where rp.name = 'sysadmin'
order by mp.name;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-admins