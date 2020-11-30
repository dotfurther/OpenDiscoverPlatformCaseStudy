# Open Discover Platform Case Study
## Open Discover Platform is a higher level of document content extraction/processing built upon the Open Discover SDK for .NET. 
### This repository show cases the following:
  - Using the Open Discover Platform API to process the Enron Microsoft Outlook PST Data Set published by EDRM and ZL Technologies, Inc.   
  - Using [RAVENDB 5.1](https://ravendb.net/) document database to store, index, and query the output produced by the Open Discover Platform API. RAVENDB 5.1 now allows for text attachments to be indexed; however, for this case study extracted text will be stored as a document record property and indexed. 
  - .NET WPF demo application that uses custom RAVENDB indexes to query and display:
     - Summaries of a document counts, file types, file sizes
     - Charts of all documents counts by a "SortDate" (SortDate is a date calculated from either document metadata or document file system properties, and it usually represents the date the document owner last modified the document).
     - Summary of all languages found in all documents in the data set.
     - Summary of all sensitive items/entities found in all documents in the data set
     - Full-text search using RAVENDB
     - Searching for all documents that have a specific type of sensitive item (e.g., search for all documents with a bank account or IBAN numbers).
### We chose the Enron Microsoft Outlook PST Data Set for the following reasons:
- It is a common benchmark dataset used in legal/eDiscovery/Information Governance industries (mostly for comparing document/attachment counts, de-duplication, and relative processing/indexing speeds)
- This data set still has, even after rounds of personally identifiable information cleansing, MUCH sensitive item information (PII) such as credit card numbers, social security numbers, IBAN accounts, investment account numbers, driver's licenses, and much more. Since it is an 'old' dataset (~20 years), and it is a publicly available dataset, those effected by the loss of personal information were long ago notified.
### Open Discover Platform API comes with class DocumentTaskEngine that is purposed for multi-threaded processing of sets of documents (typically a set is 1000-5000 documents at a time). In this case study, a single instance of DocumentTaskEngine was used to 'process' the Enron Outlook PST dataset. 'Processing' a set of documents includes:
- Identifying the file format types of each document
- Hashing the document bytes or content
- de-NIST-ing the documents (that is comparing each document hash to a ~100M known NIST hash database of common/known files). 
- Extracting document text, metadata, and attributes
- Identifying the languages present in the extracted text
- Optionally, identifying sensitive items and entities present in the extracted text. Sensitive items includes social security numbers, credit card numbers, bank account numbers, investment account numbers, IBAN, addresses, phone numbers, driver's license numbers, vehicle identification numbers (VIN), health care member numbers, and more
- If a document has an attachment or embedded item, then the attachment is also processed through the above steps 

A single instance of DocumentTaskEngine is typically capable of processing document sets at 40-70 GB/hour rate* (* rates will be dependent on user hardware and file types in the dataset). It is very fast at processing documents while also extracting more content than most eDiscovery software (e.g., sensitive item detection and de-NIST-ing while processing).
Screen shots of the PlatformAPIDemo.exe, a user interface that 'wraps' one DocumentTaskEngine instance, are shown at the end us this case study. The PlatformAPIDemo.exe example application was used to process all the Enron data in this case study. 

The PlatformAPIDemo.exe along with C# example projects for bulk inserting into RAVENDB, creating advanced RAVEBDB indexes, creating load files from Platform output, and Lucene indexing Platform output are distributed to companies that demo the Open Discover Platform and SDK. 

In addition to the Open Discover Platform API, a 3rd party partner has developed a processing job management system (JMS) that manages distributed DocumentTaskEngine instances (and OCR worker instances) whether on separate desktops, virtual machines, or Azure Docker containers. If you are in the legal/eDiscovery/information governance industries (or if your company routinely processes large volumes of documents) and are interested in demo-ing the JMS/Open Discover Platform then contact us at https://dotfurther.com/contact-us/.

### Lets take a quick look at the content that Open Discover Platform API extracted from the Enron Outlook PST dataset and which got bulk inserted into a RAVEDB document store
This screen shot shows an email (and its attachments) that were extracted and processed from one of the Enron Outlook PSTs. Note the calculated "SortData", document hashes, and metadata

<img src="Image1.jpg">

Email specific content like all recipients and extra hashes:

<img src="Image2.jpg">

This email screen shot shows a bank account number that was extracted/identified as a "sensitive item":

<img src="image3.jpg">

Some "entities" found in another email:

<img src="image4.jpg">



