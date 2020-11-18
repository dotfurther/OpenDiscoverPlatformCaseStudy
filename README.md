# Open Discover Platform Case Study
Open Discover Platform is a higher level of document content extraction built upon the Open Discover SDK for .NET. This repository will show case the content extraction processing and storage of the following:
- using the Open Discover Platform API to process the Enron Microsoft Outlook PST Data Set published by EDRM and ZL Technologies, Inc.  
- using a powerful document database such as ravendb to store, index, and query the output produced by the Open Discover Platform API.
We chose the Enron Microsoft Outlook PST Data Set for several reasons:
- It is a common benchmark dataset in eDiscover/Information governance (mostly for comparing document/attachment counts and processing speeds)
- It still has, after rounds of personally identifiable information cleansing, much sensitive item information (PII) such as credit card numbers, social security numbers, IBAN accounts, investment account numbers, driver's licenses, and much more. Since it is an 'old' dataset (~20 years), and it is a publicly available dataset, those effected by the loss of personal information were long ago notified.
