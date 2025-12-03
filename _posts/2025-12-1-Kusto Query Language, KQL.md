---
title: "Kusto Query Language, KQL"
categories: knowledge
permalink: /blogs/kql
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
#classes: wide
author_profile: false
---

> This is a resource on Kusto Query Language, KQL. It is language generally used for Microsoft cloud products for System performance, user activity, device health, compliance and security. Microsoft security tools such as Microsoft Defender suite of security tools, Microsoft Azure Active Directory, Microsoft Defender suite and many more. KQL is WORM language, write once read many. Microsoft Sentinel SIEM uses KQL for example in SOC environments. 

Almost all modern SOC tools use a query language.

KQL → Microsoft Sentinel, Defender XDR

SPL → Splunk

QL → Elastic, Humio, Chronicle, Sumo Logic

Sigma rules → universal detection rules

YARA-L → detection logic on EDR tools


KQL materials.

Azure Data Explorer Free Cluster
The Azure Data Explorer free cluster is a no-cost, fully managed environment designed to help users learn and explore Kusto Query Language (KQL). It provides a quick and easy way to run queries, ingest sample data, and experiment with powerful analytics features—without needing to set up or pay for infrastructure. Ideal for beginners and learners, it supports hands-on practice for scenarios like log analytics, telemetry analysis, and interactive data exploration.

https://learn.microsoft.com/en-us/azure/data-explorer/start-for-free-web-ui

# 📁 Resources 

## KQL Video Series

I watched this entire YouTube playlist by to learn KQL.

[https://www.youtube.com/watch?v=4VezNFqMnpg&list=PLuIShsT8L3sCjndVr4iwT4Uyh6aquB3q2&index=1](https://www.youtube.com/watch?v=4VezNFqMnpg&list=PLuIShsT8L3sCjndVr4iwT4Uyh6aquB3q2&index=1)

## Queries Practice (unorganized)<br>
Ep3. <br>
WHERE<br>
TAKE<br>
| = PIPE

Customers<br>
| where FirstName == "Peter"<br>
| where ContinentName == "Europe"<br>
| where Education == "Graduate Degree"

Products<br>
| take 10

cluster('help').database('SecurityLogs').Email<br>
| take 10

cluster('help').database('Samples').PopulationData<br>
| where State == "ARKANSAS"


Ep4.
// comment<br>
spaces dont matter<br>
=~ Case insensitive<br>
"" or ''<br>
!= Does not equal

Ep5.
contains (case insensitive and include only portions of strings)<br>
has (looks for full strings, but can use delimiters and is not case sensitive)<br>
Delimiters examples: /.[{(,spaces <br>
starts with<br>
ends with<br>
can be used with !<br>
ie; !startswith_cs means doesnot startwith and case sensitive

has vs contains: if search for http, contains would show http and https, whereas if search for http, has only shows http and not https

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where url contains "envolvelabs"

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where user_agent contains "Firefox"

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where url has "envolvelabs"

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where src_ip startswith "145"

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where url endswith "home"

cluster('help').database('SecurityLogs').OutboundBrowsing<br>
| where url has "http"

cluster('help').database('SecurityLogs').InboundBrowsing<br>
| where user_agent has "iphone"

Ep6. 

cluster('help').database('SecurityLogs').ProcessEvents<br>
| where process_name == 'excel.exe'<br>
| sort by hostname asc

cluster('help').database('SecurityLogs').ProcessEvents<br>
| where process_name == 'excel.exe'<br>
| sort by hostname desc

cluster('help').database('SecurityLogs').ProcessEvents<br>
| where process_name == 'excel.exe'<br>
| sort by timestamp desc 

cluster('help').database('SecurityLogs').ProcessEvents<br>
| where process_name == 'excel.exe'<br>
| sort by parent_process_name asc, process_hash asc 

cluster('help').database('SecurityLogs').ProcessEvents<br>
| where process_name == 'excel.exe'<br>
| order by parent_process_name asc, process_hash asc <br>
| distinct parent_process_name, process_hash

cluster('help').database('SecurityLogs').Employees<br>
| where role == 'IT associate'<br>
| sort by name asc 

cluster('help').database('SecurityLogs').Employees<br>
| where role == 'IT associate'<br>
| count 

cluster('help').database('Samples').nyc_taxi<br>
| count 

cluster('help').database('Samples').nyc_taxi<br>
| take 10

cluster('help').database('Samples').nyc_taxi<br>
| where tip_amount == "0"<br>
| count

cluster('help').database('ContosoSales').SalesTable<br>
| take 10

cluster('help').database('ContosoSales').SalesTable<br>
| distinct Country, State<br>
| sort by Country asc, State asc <br>
| count 

cluster('help').database('ContosoSales').SalesTable<br>
| distinct Country//, State<br>
//| sort by Country asc, State asc <br>
| count 

cluster('help').database('SecurityLogs').Employees<br>
| take 10

cluster('help').database('SecurityLogs').Employees<br>
| sort by role asc, name asc <br>
//| project name, role

Ep7.

https://portal.azure.com/#view/Microsoft_OperationsManagementSuite_Workspace/LogsDemo.ReactView

aka.ms/lademo

log analytics workspace environment

VMComputer<br>
| take 10

project = only shows the fields we want. Use at the end of query

VMComputer<br>
| project TimeGenerated, Hostname, OperatingSystemFamily, Cpus, CpuSpeed


VMComputer<br>
| where OperatingSystemFamily == "windows"<br>
| where Cpus == "4"<br>
| project TimeGenerated, Hostname, OperatingSystemFamily, Cpus, CpuSpeed

VMComputer<br>
| where OperatingSystemFamily == "windows"<br>
| where Cpus >= 2<br>
| project TimeGenerated, Hostname, OperatingSystemFamily, Cpus, CpuSpeed


Microsoft Sentinel

SecurityEvent<br>
| take 10

project-reorder = orders the fields first, and the remaining fields are shown on the right side of the fields

SecurityEvent<br>
| project-reorder Activity, Process, AccountType<br>
| take 10

rename fields

SecurityEvents<br>
| project Process, ProcessCode=Activity, AccountType<br>
| take 10

VMConnection<br>
| take 10

VMConnection<br>
| where DestinationPort == "443"<br>
| project RemoteIP, RemoteCountry

VMConnection<br>
| where DestinationPort == "443"<br>
| where Remotecountry == "Sweden"<br>
//| distinct RemoteCountry<br>
| project RemoteIP, RemoteCountry

Usage<br>
| where Quantity >= 10<br>
| project Quantity, Units=QuantityUnit, DataType

Ep8.<br>
Limit<br>
Top<br>
Boolean (and , or)

| where FirtName == "Peter"<br>
  and Education == "High School"<br>
  and CityName == "Lieusaint"<br>
| project FirstName, Lastname

VMConnection <br>
| where ProcessName == "python3"<br>
	or SourceIP == "127.0.0.1"

WindowsFirewall<br>
| where (destinationPort == '80' and Protocol == 'TCP') or DestinationIP startswith '20'<br>
project DestinationPort, Protocol, DestinationIP

'*' = used for probing

VMConnection<br>
| where * has '389'

limit = same like take

VMConnection<br>
| where * has '389'<br>
| order by SourceIP asc<br>
| limit 10

top 10 = first 10

take = random records

VMConnection<br>
| where * has '389'<br>
| top 10 by TimeGenerated desc

SigninLogs<br>
| top 10 by TimeGenerated desc<br>
//| take 10

VMConnection<br>
| where RemoteLatitude >= 60 or ResponseTimeMax > 1000<br>
| project RemoteLatitude, ResponseTimeMax

WindowsFirewall<br>
| where Destinationport == '80' and Protocol == 'TCP'<br>
| count

Ep9.

Time

SigninLogs<br>
| where TimeGenerated >= ago(10d)<br>
// means 10 days ago, greater than, which is newer than 10 days ago

d = Day, h = Hour m= Minute s=Second

SigninLogs<br>
| where TimeGenerated < ago(4h)<br>
// means 4 hours ago, less than, which is older than 4 hours ago

SigninLogs<br>
| where TimeGenerated betweeen (datetime(2023-7-5T02:00:00) .. datetime(2023-7-6T04:00:00))<br>
| sort by TimeGenerated desc

SigninLogs<br>
| where TimeGenerated betweeen (datetime(2023-7-3) .. now())<br>
| sort by TimeGenerated desc

SigninLogs<br>
| where TimeGenerated betweeen (datetime(2023-7-3) .. (now() -4h))<br>
| sort by TimeGenerated desc

VMProcess<br>
| take 10

VMConnection<br>
| take 10

VMConnection<br>
| where TimeGenerated >= ago(7d)<br>
 and DestinationPort == '80' <br>
 and Computer == 'AppArcWin'<br>
| distinct ProcessName

Homework:

Perf<br>
//|take 10<br>
| where TimeGenerated >= ago(3d)<br>
 and CounterName contains "Bytes sent" <br>
 and CounterValue > 10000 <br>
| sort by CounterValue desc<br>
| project TimeGenerated, CounterName, CounterValue

Ep 10.

getschema , extend, search

search in (ContainerLog,)

SigninLogs<br>
| search "Azure Portal"

SigninLogs<br>
| where * has "Azure Portal"

SigninLogs<br>
| search "*Azure Portal"

SigninLogs
| search "*Azure Portal*"

SigninLogs<br>
| search Location: "FR" or AppDisplayName: "Azure"

search "40.78.229.33"<br>
//can see new field, $table

search "40.78.229.33"<br>
| distinct $table

search "40.78.229.33"<br>
| where DestPublicIPs_s contains "40.78.229.33"<br>
| project TimeGenerated, DestPublicIPs_s<br>
//| distinct $table

search "YouTube"<br>
| where TimeGenerated > datetime(2023-07-15)<br>
| sort by TimeGenerated desc

search in (ContainerLog, AVSSyslog) "google"

Usage<br>
| take 10

extend = add a new field

Usage<br>
| extend GB=Quantity/1000<br>
| sort by GB desc

getschema = see DataType

ContainerInventory<br>
| getschema

Homework:

search "185.125.190.23"<br>
| where TimeGenerated >= ago(3d)<br>
| distinct $table

## Conclusion

- Overall learning KQL is similar to SQL. It is easy and straightforward to learn. 

