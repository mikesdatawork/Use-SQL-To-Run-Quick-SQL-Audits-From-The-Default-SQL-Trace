![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Use SQL To Run Quick SQL Audits From The Default SQL Trace
**Post Date: April 23, 2014**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's a script which will help you extract information from the default trace. This should server as a quick audit query, and not a long term audit solution. You can modify the logic to include object names, etc.</p>      


## SQL-Logic
```SQL
declare @trace_path varchar(max)
set @trace_path = ( select path from sys.traces ) select
'for server' = servername
, 'user name' = loginname
, 'from device' = hostname
, 'started on' = convert(char, starttime, 9) , 'using app' = applicationname , 'in database' = databasename
--, 'affected object' = object_name(objectid) , 'object type' = case objecttype
when '8259' then 'Check Constraint'
when '8260' then 'Default (constraint or standalone)'
when '8262' then 'Foreign-key Constraint'
when '8272' then 'Stored Procedure'
when '8274' then 'Rule'
when '8275' then 'System Table'
when '8276' then 'Trigger on Server'
when '8277' then '(User-defined) Table'
when '8278' then 'View'
when '8280' then 'Extended Stored Procedure'
when '16724' then 'CLR Trigger'
when '16964' then 'Database'
when '16975' then 'Object'
when '17222' then 'FullText Catalog'
when '17232' then 'CLR Stored Procedure'
when '17235' then 'Schema'
when '17475' then 'Credential'
when '17491' then 'DDL Event'
when '17741' then 'Management Event'
when '17747' then 'Security Event'
when '17749' then 'User Event'
when '17985' then 'CLR Aggregate Function'
when '17993' then 'Inline Table-valued SQL Function'
when '18000' then 'Partition Function'
when '18002' then 'Replication Filter Procedure'
when '18004' then 'Table-valued SQL Function'
when '18259' then 'Server Role'
when '18263' then 'Microsoft Windows Group'
when '19265' then 'Asymmetric Key'
when '19277' then 'Master Key'
when '19280' then 'Primary Key'
when '19283' then 'ObfusKey'
when '19521' then 'Asymmetric Key Login'
when '19523' then 'Certificate Login'
when '19538' then 'Role'
when '19539' then 'SQL Login'
when '19543' then 'Windows Login'
when '20034' then 'Remote Service Binding'
when '20036' then 'Event Notification on Database'
when '20037' then 'Event Notification'
when '20038' then 'Scalar SQL Function'
when '20047' then 'Event Notification on Object'
when '20051' then 'Synonym'
when '20307' then 'Sequence'
when '20549' then 'End Point'
when '20801' then 'Adhoc Queries which may be cached'
when '20816' then 'Prepared Queries which may be cached'
when '20819' then 'Service Broker Service Queue'
when '20821' then 'Unique Constraint'
when '21057' then 'Application Role'
when '21059' then 'Certificate'
when '21075' then 'Server'
when '21076' then 'Transact-SQL Trigger'
when '21313' then 'Assembly'
when '21318' then 'CLR Scalar Function'
when '21321' then 'Inline scalar SQL Function'
when '21328' then 'Partition Scheme'
when '21333' then 'User'
when '21571' then 'Service Broker Service Contract'
when '21572' then 'Trigger on Database'
when '21574' then 'CLR Table-valued Function'
when '21577' then 'Internal Table (For example, XML Node Table, Queue Table.)'
when '21581' then 'Service Broker Message Type'
when '21586' then 'Service Broker Route'
when '21587' then 'Statistics'
when '21825' then 'User'
when '21827' then ''
when '21831' then ''
when '21843' then ''
when '21847' then ''
when '22099' then 'Service Broker Service'
when '22601' then 'Index'
when '22604' then 'Certificate Login'
when '22611' then 'XMLSchema'
when '22868' then 'Type' end
, 'text extracted' = textdata
from
fn_trace_gettable(@trace_path, 1)
where
databasename is not null
and objecttype is not null
and objecttype not in
(
'21587' -- Statistics
, '21827' --
, '21831' --
, '21843' --
, '21847' -- ) and databasename not in ('master', 'model', 'msdb', 'tempdb')
```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

   
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

