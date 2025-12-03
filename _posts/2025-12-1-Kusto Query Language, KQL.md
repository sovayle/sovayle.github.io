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

## Notes (unorganized)
Ep3. 
WHERE
TAKE
| = PIPE

Customers
| where FirstName == "Peter"
| where ContinentName == "Europe"
| where Education == "Graduate Degree"

Products
| take 10

cluster('help').database('SecurityLogs').Email
| take 10

cluster('help').database('Samples').PopulationData
| where State == "ARKANSAS"


Ep4.
// comment
spaces dont matter
=~ Case insensitive
"" or ''
!= Does not equal

Ep5.
contains (case insensitive and include only portions of strings)
has (looks for full strings, but can use delimiters and is not case sensitive)
Delimiters examples: /.[{(,<spaces
starts with
ends with
can be used with !
ie; !startswith_cs means doesnot startwith and case sensitive

has vs contains: if search for http, contains would show http and https, whereas if search for http, has only shows http and not https

cluster('help').database('SecurityLogs').InboundBrowsing
| where url contains "envolvelabs"

cluster('help').database('SecurityLogs').InboundBrowsing
| where user_agent contains "Firefox"

cluster('help').database('SecurityLogs').InboundBrowsing
| where url has "envolvelabs"

cluster('help').database('SecurityLogs').InboundBrowsing
| where src_ip startswith "145"

cluster('help').database('SecurityLogs').InboundBrowsing
| where url endswith "home"

cluster('help').database('SecurityLogs').OutboundBrowsing
| where url has "http"

cluster('help').database('SecurityLogs').InboundBrowsing
| where user_agent has "iphone"

Ep6. 

cluster('help').database('SecurityLogs').ProcessEvents
| where process_name == 'excel.exe'
| sort by hostname asc

cluster('help').database('SecurityLogs').ProcessEvents
| where process_name == 'excel.exe'
| sort by hostname desc

cluster('help').database('SecurityLogs').ProcessEvents
| where process_name == 'excel.exe'
| sort by timestamp desc 

cluster('help').database('SecurityLogs').ProcessEvents
| where process_name == 'excel.exe'
| sort by parent_process_name asc, process_hash asc 

cluster('help').database('SecurityLogs').ProcessEvents
| where process_name == 'excel.exe'
| order by parent_process_name asc, process_hash asc 
| distinct parent_process_name, process_hash

cluster('help').database('SecurityLogs').Employees
| where role == 'IT associate'
| sort by name asc 

cluster('help').database('SecurityLogs').Employees
| where role == 'IT associate'
| count 

cluster('help').database('Samples').nyc_taxi
| count 

cluster('help').database('Samples').nyc_taxi
| take 10

cluster('help').database('Samples').nyc_taxi
| where tip_amount == "0"
| count

cluster('help').database('ContosoSales').SalesTable
| take 10

cluster('help').database('ContosoSales').SalesTable
| distinct Country, State
| sort by Country asc, State asc 
| count 

cluster('help').database('ContosoSales').SalesTable
| distinct Country//, State
//| sort by Country asc, State asc 
| count 

cluster('help').database('SecurityLogs').Employees
| take 10

cluster('help').database('SecurityLogs').Employees
| sort by role asc, name asc 
//| project name, role

## Conclusion

- Overall learning KQL is similar to SQL. It is easy and straightforward to learn. 

