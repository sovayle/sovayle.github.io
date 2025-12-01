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

> This is a resource on Kusto Query Language, KQL. It is language generally used for Microsoft products such as Microsoft security tools, Microsoft Azure and many more. Microsoft Sentinel SIEM uses KQL for example in SOC environments. 

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


## Conclusion

- Overall learning KQL is similar to SQL. It is easy and straightforward to learn. 

