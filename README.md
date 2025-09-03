# Inprogress

```
select * ,
CASE 
When subject like '%Rancher%' then 'user monitoring'
ELSE 'default_result'
END as raj
from finalop
order by ticket;
```
