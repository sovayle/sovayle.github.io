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


KQL materials.

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


eP4.
// comment
spaces dont matter
=~ Case insensitive
"" or ''


## Conclusion

- Overall learning KQL is similar to SQL. It is easy and straightforward to learn. 

