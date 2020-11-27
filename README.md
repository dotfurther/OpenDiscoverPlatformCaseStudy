# Open Discover Platform Case Study
## Open Discover Platform is a higher level of document content extraction/processing built upon the Open Discover SDK for .NET. 
### This repository will show case the following:
- Using the Open Discover Platform API to process a subset of the Enron Microsoft Outlook PST Data Set published by EDRM and ZL Technologies, Inc.  
- Using a powerful document database such as [RAVENDB 5.1](https://ravendb.net/) to store, index, and query the output produced by the Open Discover Platform API.
### We chose the Enron Microsoft Outlook PST Data Set for the following reasons:
- It is a common benchmark dataset in eDiscovery/legal/Information Governance industries (mostly for comparing document/attachment counts, de-duplication, and relative processing/indexing speeds)
- This data set still has, even after rounds of personally identifiable information cleansing, MUCH sensitive item information (PII) such as credit card numbers, social security numbers, IBAN accounts, investment account numbers, driver's licenses, and much more. Since it is an 'old' dataset (~20 years), and it is a publicly available dataset, those effected by the loss of personal information were long ago notified.
