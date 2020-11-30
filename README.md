# Open Discover Platform Case Study
## Open Discover Platform is a higher level of document content extraction/processing built upon the Open Discover SDK for .NET. 
### This repository show cases the following:
  - Using the Open Discover Platform API to process the Enron Microsoft Outlook PST Data Set published by EDRM and ZL Technologies, Inc.   
  - Using a document database to store, index, and query the output produced by the Open Discover Platform API. In the study we use [RAVENDB 5.1](https://ravendb.net/) as our document database. RAVENDB 5.1 now allows for text attachments to be indexed; however, for this case study extracted text will be stored as a document record property and indexed. 
  - .NET WPF demo application (a C# project available to those that demo Open Discover Platform) that uses custom RAVENDB indexes to query and display:
     - Summaries of a document counts, file types, file sizes
     - Charts of all documents counts by a "SortDate" (SortDate is a date calculated from either document metadata or document file system properties, and it usually represents the date the document owner last modified the document).
     - Summary of all languages found in all documents in the data set.
     - Summary of all sensitive items/entities found in all documents in the data set
     - Full-text search using RAVENDB
     - Searching for all documents that have a specific type of sensitive item (e.g., search for all documents with a bank account or IBAN numbers).
     - Many features of an early case assesment (ECA) application
  - Open Discover API + document store such as RAVENDB or Elasticsearch leads to fast, easy, and powerful full-text search/eDiscovery/Information governance applications   
### We chose the Enron Microsoft Outlook PST Data Set for the following reasons:
- It is a common benchmark dataset used in legal/eDiscovery/Information Governance industries (mostly for comparing document/attachment counts, de-duplication, and relative processing/indexing speeds)
- This data set still has, even after rounds of personally identifiable information cleansing, MUCH sensitive item information (PII) such as credit card numbers, social security numbers, IBAN accounts, investment account numbers, driver's licenses, and much more. Since it is an 'old' dataset (~20 years), and it is a publicly available dataset, those effected by the loss of personal information were long ago notified.
### Open Discover Platform API is purposed for multi-threaded processing of sets of documents (typically a set is 1000-5000 documents at a time). 'Processing' a set of documents includes:
- Identifying the file format types of each document
- Hashing the document bytes or content
- de-NIST-ing the documents (that is comparing each document hash to a ~100M known NIST hash database of common/known files). 
- Extracting document text, metadata, and attributes
- Identifying the languages present in the extracted text
- Optionally, identifying sensitive items and entities present in the extracted text. Sensitive items includes social security numbers, credit card numbers, bank account numbers, investment account numbers, IBAN, addresses, phone numbers, driver's license numbers, vehicle identification numbers (VIN), health care member numbers, and more
- If a document has an attachment or embedded item, then this child item is also processed through the above steps, this continues until no more child documents are left to process

Open Discover Platform API is typically capable of processing document sets at 40-70 GB/hour rate* (* rates will be dependent on user hardware and file types in the dataset). It is very fast at processing documents while also extracting more content than most eDiscovery software (e.g., sensitive item/entity detection and de-NIST-ing while processing).
Screen shots of the PlatformAPIDemo.exe, a user interface that 'wraps' one Open Discover Platform API instance, are shown at the end us this case study. The PlatformAPIDemo.exe example application was used to process all the Enron Outlook PST data in this case study. 

The PlatformAPIDemo.exe along with C# example projects for bulk inserting into RAVENDB, advanced RAVEBDB indexes, creating eDiscovery load files from Platform API output, and Lucene indexing Platform API output are distributed to companies that demo the Open Discover Platform and SDK. 

In addition to the Open Discover Platform API, a 3rd party partner has developed a processing job management system (JMS) that manages distributed DocumentTaskEngine instances (and OCR worker instances) whether on separate desktops, virtual machines, or Azure Docker containers. If you are in the legal/eDiscovery/information governance industries (or if your company routinely processes large volumes of documents) and are interested in demo-ing the JMS/Open Discover Platform then contact us at https://dotfurther.com/contact-us/.

### Quick look example content that Open Discover Platform API extracted from the Enron Outlook PST dataset (i.e., the content which was bulk inserted into a RAVEDB document store):
The below screen shot shows an email (and its attachments) that was extracted and processed from one of the Enron Outlook PSTs. Note the calculated "SortDate" and document hashes and the extracted metadata:

<img src="Image1.jpg">

Email specific content like all recipients and extra hashes:

<img src="Image2.jpg">

This email screen shot shows a bank account number that was extracted/identified as a "sensitive item" in the email's extracted text (extracted text and metadata are scanned for sensitive items):

<img src="image3.jpg">

Some "entities" identified in a different email:

<img src="image4.jpg">

### Query the RAVEDB document



