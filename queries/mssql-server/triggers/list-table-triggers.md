# List table triggers in SQL Server database

Query below lists tables with their triggers.


``` sql
select schema_name(tab.schema_id) + '.' + tab.name as [table],
    trig.name as trigger_name,
    case when is_instead_of_trigger = 1 then 'Instead of'
        else 'After' end as [activation],
    (case when objectproperty(trig.object_id, 'ExecIsUpdateTrigger') = 1 
            then 'Update ' else '' end
    + case when objectproperty(trig.object_id, 'ExecIsDeleteTrigger') = 1 
            then 'Delete ' else '' end
    + case when objectproperty(trig.object_id, 'ExecIsInsertTrigger') = 1 
            then 'Insert ' else '' end
    ) as [event],
    case when trig.[type] = 'TA' then 'Assembly (CLR) trigger'
        when trig.[type] = 'TR' then 'SQL trigger' 
        else '' end as [type],
    case when is_disabled = 1 then 'Disabled'
        else 'Active' end as [status],
    object_definition(trig.object_id) as [definition]
from sys.triggers trig
    inner join sys.objects tab
        on trig.parent_id = tab.object_id
order by schema_name(tab.schema_id) + '.' + tab.name, trig.name;
	
```

ref: https://dataedo.com/kb/query/sql-server/list-table-triggers