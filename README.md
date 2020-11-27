# Open Discover Platform Case Study
## Open Discover Platform is a higher level of document content extraction/processing built upon the Open Discover SDK for .NET. 
### This repository will show case the following:
- Using the Open Discover Platform API to process a subset of the Enron Microsoft Outlook PST Data Set published by EDRM and ZL Technologies, Inc.  
- Using [RAVENDB 5.1](https://ravendb.net/) to store, index, and query the output produced by the Open Discover Platform API. RAVENDB 5.1 now allows for text attachments to
be indexed; however for this case study extracted from emails and office documents will be stored as a document property and indexed. 
### We chose the Enron Microsoft Outlook PST Data Set for the following reasons:
- It is a common benchmark dataset used in eDiscovery/legal/Information Governance industries (mostly for comparing document/attachment counts, de-duplication, and relative processing/indexing speeds)
- This data set still has, even after rounds of personally identifiable information cleansing, MUCH sensitive item information (PII) such as credit card numbers, social security numbers, IBAN accounts, investment account numbers, driver's licenses, and much more. Since it is an 'old' dataset (~20 years), and it is a publicly available dataset, those effected by the loss of personal information were long ago notified.
### Open Discover Platform API comes with class DocumentTaskEngine that is used for processing a set of documents (typically 1000-5000 documents at a time). Processing a set of documents includes:
- Identifying the file format types of each document
- Hashing the document bytes or content
- de-NIST-ing the documents (that is comparing to ~100M known NIST hashes of common/known files)
- Extracting document text, metadata, and attributes
- Identifying the languages present in the extracted text
- Optionally, identifying sensitive items and entities present in the extracted text. Sensitive items includes social security numbers, credit card numbers, bank account numbers, investment account numbers, IBAN, addresses, phone numbers, driver's license numbers, vehicle identification numbers (VIN), health care member numbers, and more
- If a document has an attachment or embedded item, then the attachment is also processed through the above steps 
