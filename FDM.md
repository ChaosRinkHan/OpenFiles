# Overview

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Data formats](#data-formats)
  - [Data format](#data-format)
  - [I/O](#io)
  - [Lustre](#lustre)
  - [File system](#file-system)
  - [XML & JSON](#xml--json)
  - [Metadata](#metadata)
  - [Persistent Identifiers PID](#persistent-identifiers-pid)
- [Database](#database)
  - [Relational Databases](#relational-databases)
  - [NoSQL Databases](#nosql-databases)
  - [RDF Database](#rdf-database)
- [Semantic data](#semantic-data)
  - [RDF](#rdf)
  - [SPARQL](#sparql)
- [Data lifecycle, DMP](#data-lifecycle-dmp)
  - [Components](#components)
  - [Data management planning](#data-management-planning)
- [Law](#law)
  - [How to use a dataset](#how-to-use-a-dataset)
  - [GDPR](#gdpr)
- [Archiving and preservation](#archiving-and-preservation)
  - [OAIS](#oais)
- [Data infrastructure and hardware](#data-infrastructure-and-hardware)
  - [Storage architecture](#storage-architecture)
- [MapReduce](#mapreduce)
  - [Map](#map)
  - [Reduce](#reduce)
  - [Process](#process)
- [Hadoop](#hadoop)
  - [vs MPI/HPC](#vs-mpihpc)
  - [Apache Spark](#apache-spark)
- [Data streaming](#data-streaming)
  - [ML techniques](#ml-techniques)
- [Blockchain](#blockchain)
  - [What](#what)
  - [Good use case](#good-use-case)
  - [Hyperledger Fabric](#hyperledger-fabric)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Data formats 

Digital data: encoding, file format, files, records

-   Encoding: interpreting groups of bits 

-   Endian: big, little 
-   Unicode, UTF

-   Format: interpreting **decoded** bit groups (bytes, characters) 

-   File: basic unit of data organisation. Pointer, metadata.
-   Files vs objects
    -   Object storage is becoming more **common** – especially in “big data” contexts, match with http/REST model of resources on the Web 
    -   Metadata: 
        -   File: central location using fixed schema, scalability becomes an issue
        -   Objects: metadata bundled with content with flexible schema, scalability much better 

|             | File                                          | Objects                                   |
| ----------- | --------------------------------------------- | ----------------------------------------- |
| Metadata    | stored in central location using fixed schema | bundled with content with flexible schema |
| Findability | straight forward (read the inode table)       | can be a challenge                        |
| Scalability | becomes an issue                              | much better                               |

## Data format

### HDF5

**Hierarchical Data Format (version 5)**

Binary but portable

>   *HDF5 is a unique technology suite that makes possible the management of extremely **large** and **complex** data collections.* 

A versatile **data model** that can represent very complex data objects and a wide variety of metadata.

A completely **portable file format** with no limit on the number or size of data objects in the collection.

A software **library** that runs on a range of computational platforms

A rich set of integrated **performance** features that allow for access time and storage space optimizations.

**Tools** and **applications** for managing, manipulating, viewing, and analyzing the data in the collection.

-   Based on *groups* and *datasets*
    -   Structure
    -   Portability
    -   Performance
    -   Free & Open Source
-   Group: header, symbol label
-   Datasets: header, data array

#### Parallel HDF5 

-   Designed to work with MPI and MPI-IO 



#### CDF: Binary and portable 

### netCDF

**Net**work **C**ommon **D**ata **F**ormat (• Data model • File format • API • Library implementing the API)

**Portable binary** format with a rich set of libraries.

The netCDF niche is **array-oriented scientific** data.

netCDF files:

-   **Variables**: N-dimensional arrays of char, byte, short, int, float, double 
-   **Dimensions**: Name and length 
-   **Attributes**: Annotations and other metadata 
    -   Name
    -   Type (same as variable types)
    -   Values 
-   Pathname`*`
-   Data values



-   **Groups**: Hierarchical, similar to directories 
-   User-defined **types** 

#### CDL (Common Data Language)

Human readable notation for NetCDF datasets and data 

#### High-performance NetCDF

##### Enhanced NetCDF (version 4 and beyond) 

• Built on HDF5 for parallel/high performance I/O • Files need to be stored in HDF5 format 

#### PNetCDF

Support parallel I/O 

### What to use

-   If raw **performance** is biggest issue for you: MPI-I/O

-   If **metadata/storage** format is biggest issue for you: HDF5 

-   If you want to integrate with earth **science** tools: NetCDF 

## I/O

![image-20191213153628155](https://i.imgur.com/jEeZRpG.png)

-   MPI-I/O
    -   Provide distributed access to single file

## Lustre

-   Object Storage: OSS -> OST
-   Metadata; MDS -> MDT

## File system

-   GPFS IBM’s General Parallel File System `*`
-   AFS
-   POSIX I/O 
-   Lustre open source parallel file system `*`
-   HDFS Hadoop file system `*`

`*`: high performance file system 

## XML & JSON

### Why?

-   Mainly used for platform and language neutral data **exchange** and **storage** 
    -   Both text based 
-   Many **web services** support both XML and JSON based request and responses 
-   Both used for **storing** application data 

### XML

eXtensible Markup Language 

XML can be use to store an application **configuration** and **state**.

-   Declaraition  `<?xml version="1.0" encoding="UTF-8"?>`
-   Tags: text in between < and > 
-   Elements
    -   Start tag and an end tag defines an element 
    -   Could be self contains, e.g.,` <self/>`
    -   XML document contains one root element 
-   Attributes 
    -   Name-value pairs that provide additional information about an element. 
    -   Can use either single or double quotes to encode values 
    -   Each attribute name is unique within the same element 

Many Web Services are described using WSDL.

#### WSDL 

Web Services Description Language 

-   Operations and data input/output to a web service are described using XML 
-   Can generate a web service application **skeleton** using a WSDL 

#### SOAP

Simple Object Access Protocol

-   An XML based communication protocol 
-   Allows platform neutral communication between different applications, usually over http 
-   Typically, WSDL based web services communicate **using** SOAP messages 

#### Validation: XML schemas

Describes the valid structure and content for a XML document.

-   W3C XML schemas
-   DTD Document Type Definition 

e.g. W3C schema

>   The purpose of an XML Schema is to define the legal building blocks of an XML document:
>
>   -   the elements and attributes that can appear in a document
>   -   the number of (and order of) child elements
>   -   data types for elements and attributes
>   -   default and fixed values for elements and attributes

#### Phasers

**DOM** Document Object Model

-   Reads **entire** XML document and then generates a **tree** data structure 

**SAX** Simple API for XML

-   Push parser (a.k.a, event based parsing) 
-   Suitable for reading very large XML documents 

**XPath** 

Allows navigating an XML document. Allows navigating to a specific node. W3C standard.

**XQuery** 

Allows querying an XML document. Uses XPath expressions. W3C standard.

`doc(“orders.xml”)/order/item[price<12] ` 

### JSON

JavaScript Object Notation

-   A **light weight** data exchange format
-   Much **easier** for a human to read and write than XML 

Originated from JavaScript. Supported in virtually all languages. Used for **persisting** (storing) application **objects**.

-   Commonly used in client and web server data exchanges 

#### Validation

a JSON schema describes valid content for application/domain specific JSON documents.

## Metadata

A description of what the data is. A means to *understand* the data, and possibly *reproduce* the data.

Embedded alongside the data, or in metadata files, indexes and catalogues.

### Why

-   Make your data more discoverable–to search on
-   More reusable–understandable, finding related data
-   More reproducible–know how/why/where it was collected



-   Helps data developers/users/organisations

### Good metadata

Metadata is good if it allows your data to be found and understood by all those who might want to make use of it.

-   Complete 
-   Accurate 
-   Precise 
-   Conforming to standards 
    -   Semantic: Meaning of Terms 
    -   Which metadata are mandatory 
    -   Formatting / Syntax 
-   Accessible
    -   Online, addressable (can be linked to), harvestable 

### System Metadata / Structural Metadata

File ownership, modification date, how it’s packaged, etc. 

### Content Metadata / Descriptive Metadata

– What the data relates to – Where the data relates to
– When the data relates to – Who the data relates to
– How the data were collected / created – Why the data were collected / created … 

### Create

-   Ideally the same person/people who created the data. – They understand it best! 

-   Sometimes those responsible for the data’s distribution and curation are well-placed to add additional metadata – particularly structural metadata 

### Standards

Choice depends on field of practice or motivation for using metadata.

### Semantics 

The *meaning* of the data, and how we convey this in the data and its metadata 

### Ontology 

A controlled vocabulary

-   A means to describe semantics
-   Precise definitions for a set of terms
-   Can be used in metadata and the data itself 

### Summary

-   Metadata is “data about data” or “documentation of data” 
-   Metadata allows data to be **discovered, accessed, understood and re-used** 
-   Metadata **standards** provide structure and consistency to data documentation 
-   Standards and tools vary – select according to defined criteria such as data type, organisational guidance, and available resources 
-   Standards which have associated semantics add additional value 

## Persistent Identifiers PID

### Why

Reliably refer to a particular piece of data.

Objects need to be (globally) addressable so that they can be reusable.

Once data is addressable, it can be 

-   found more easily by you, other people and computers
-   cited
-   linked together 

### What

Several different PID systems/infrastructures:

Handle System, Digital Object Identifier (DOI), Archival Resource Key (ARK), Persistent URL (PURL), Life Science Identifier (LSID), Uniform Resource Name (URN) 

### PIDs identify:

Resources (black box) e.g. data and software code; things (e.g. a species)

Normally point to what they identify.

### Characteristics 

-   Globally unique
-   Persistent over time

### Advantages 

Persistent Identity via Indirection

-   Static Identity via Indirection
-   Embedded IDs
-   Networks of Persistent Links 

### Disadvantages

-   Extra effort/cost on creation
-   Persistence requires sustained effort 
-   Analyse cost/benefit ratio 

# Database

Means of storing and accessing data efficiently 

Usually contains a Database Management System (DBMS) 

**DBMS** provides: 

- Mechanisms to **create** data structure (e.g., Tables) and content
- A means of querying and modifying content
- Ways to optimise performance
- Tools to **backup** and **restore** data 
- Ways to allow applications to access data
- Ways to **Authenticate** and **Authorise** users 

## Relational Databases 

A Collection of tables (i.e., Relations) with associated relationships 

### ER (entity relationship) diagram

-   Produces a data model representing a real-world situation 
    -   Identifies important entities (tables)
    -   **Relationship** between the **entities**. 
-   Allows **simplification** of the data model
    -   E.g., Remove many-to-many relationships 
-   Cardinality: 1-1. 1-m, m-1, m-n

### Transactions

A transaction is a **sequence** of operations performed (using one or more SQL statements) on a database as a single logical unit of work.

-   **Atomic :** A transaction is a logical unit of work which must be **either** completed with all of its data modifications, **or** none of them is performed.
-   **Consistent :** At the end of the transaction, all data must be left in a **consistent state**.
-   **Isolated :** Modifications of data performed by a transaction must be **independent** of another transaction. Unless this happens, the outcome of a transaction may be erroneous.
-   **Durable :** When the transaction is completed, effects of the modifications performed by the transaction must be **permanent** in the system.

## NoSQL Databases

Refer to non-relational databases 

-   Designed for **distributed** storage with high horizontal **scalability** 
-   No schemas are required - **flexibility**
-   No join operations - some naturally links related data – E.g., **graph** databases 
-   No ACID transactions 

------

-   **Suitable** for **scalable** **unstructured** or **semi**-structured data 
-   Also used for structured data where applications can store objects **without** any **transformations** 

### Data Models 

• Key-Value • Document • Column • Graph 

### Mongo DB

Open Source JSON-like **document** based database management system 

-   High performance
-   High availability

**Documents** contains collections of key-value pairs

4 basic CRUD operations: create, read, update, delete

Use **indexes** to support most common queries - will significantly improve performance of your queries

#### Normalised Model

Pros:

-   No **duplication** of data 

Cons: 

-   Requires **several** request for an update. First get the references. Then get the documents refer to by the references. And then update those documents 

#### De-normalised Model

Pros: 

-   **Single** document contains all interested data
-   Can be updated with single request 

Cons:

-   Data **duplication** can occur 
-   If necessary, application would need to manage potential data duplication 

## RDF Database

# Semantic data

## RDF

RDF is a data model: the **R**esource **D**escription **F**ramework 

A data model for representing semantic data 

It relies on giving every resource (every “thing”) a unique label (a URI) and describing relationships between resources with **triples**.

Information is encoded as sets of **triples**:

SUBJECT **PREDICATE** OBJECT
The cat **sat on** the mat 

-   Subject: a **resource** with a **URI**, or a **blank node** 
-   The predicate is a **resource** with a **URI** 
-   The object is
     – a **resource** with a **URI**, or – a **blank node** or
     – a literal 

## SPARQL 

SELECT, CONSTRUCT, DESCRIBE, ASK

# Data lifecycle, DMP

-   Research data management
    -   The data lifecycle **maps** well onto a typical research or experiment **timeline** 
    -   Planned and effective DM is becoming a **feature** of modern research (data science concern)
-   Product data management
    -   (Almost) synonymous with – **version control – configuration management** 
    -   Safety-critical industries may have regulatory requirements to keep versions of documents, engineering drawings etc. for decades 
-   Test data management
    -   In **data-driven service** industries (e.g. retail analytics), data used to train or develop classifiers or other insights needs to be managed in the same way 
    -   Particularly important for **provenance questions - reasoning** 

## Components

**Plan** -> acquire -> assure -> describe -> preserve -> discover -> combine -> process -> **plan** -> ...

-   Acquire: raw data, choose standard formats
-   Assure: validate, calibrate and test on data and methods
-   Describe: useful data to interpret the data (units, var. names, etc)
-   Preserve: long term storage and accessibility 
-   Discover: description, accessibility
-   Combine: combining, integrating, merging; metadata, license
-   Process: computing and data analysis

## Data management planning 

### What

-   A formal document that captures:
    -   plans for all the rest: what data will I create? how will I describe them? how will I store them? will I publish and share them? If not, why not? how will others find them? 

-   Outlines what you will do with your data **during** and **after** you complete your project 
-   Ensures your data are safe for the **present** and the **future** 

### Why

-   Saves time
     – less reorganization later 
-   Increases research efficiency 
-   Increasingly, compulsory
     – research funding agencies now ask for DMPs for most proposals 

### Components

1.  Information about **data** & data formats
2.  **Metadata** content and format
3.  **Policies** for access, sharing and re-use
4.  **Long-term** storage and data management 
5.  **Budget** 

# Law

## How to use a dataset

Copyrightable? In copyright? Covered in an exemption? Is licensed? Is covered by license? -> Contact copyright owner

## GDPR

 General Data Protection Regulation 

-   codifies & harmonises **data subject** rights 

# Archiving and preservation

## OAIS

Open Archival Information System reference model 

![image-20191214111943930](https://i.imgur.com/XdNlAqU.png)

-   Designed for **central, long-term** archives
    -   Long term
    -   Designated Community
        -   Designed for a certain group with assumptions on background, which also defines how much RI is needed
    -   Representation Information (RI): 
        -   Extra info that needs to be associated with the object so it can be understood (metadata, file formats)

# Data infrastructure and hardware

-   Amdahl number

    IO bandwidth (**bits**/s) / CPU clock rate = 1 (ideally)

-   Amdahl memory ratio

    memory size (**bytes**) / instructions per second = 1 (ideally) 

-   Building an Amdahl-balanced system

    Scale-up: increase IO throughput to match the CPU clock 

    Scale-out: power down processors to match IO throughput 

### Durability

(data durability) ~ 1 / (mean time to data loss) 

-   Redundant Arrays of Inexpensive Disks (RAID) 

## Storage architecture 

-   DAS Direct Attached Storage 

-   NAS Network Attached Storage
-   SAN Storage Area Network

# MapReduce

A parallelisation pattern suitable for distributed systems

## Map

A function is “mapped” over all of the input data. Return **a list of (key, value) pairs**

-   When you do MapReduce at scale, the Map function is run on every node where the input data resides 

## Reduce

Reduce combines data back together – a summary operation 

## Process

![image-20191214161344941](https://i.imgur.com/z3oe3hW.png)

# Hadoop

Distributed File **System** + Map Reduce **Framework** + Supporting **Functionality** 

Each Hadoop job reads data from the HDFS and writes output to the HDFS 

-   Fine for **short** chains of processing 
-   Very **inefficient** for **iterative** algorithms
-   Spark – supports **caching** data 
-   Twister – iterative map reduce 

## vs MPI/HPC

-   Fault tolerance 
    -   Hadoop is designed specifically with fault tolerance in mind 
    -   MPI provides little support for fault tolerance
-   Specific vs general
    -   Hadoop is a framework for a specific data processing pattern
    -   MPI allows you to code any algorithm you wish 

-   Iterative algorithms
    -   Hadoop very poor at multiple iterations over the data
    -   Very easy to write such programs in MPI 

-   Speed

-   Cost

    -   Hadoop simple to write and can run reliably on commodity hardware
    -   MPI typically run on expensive HPC systems 

-   Dynamic nature of data 

    -   Hadoop is good for processing massive amounts of data that is written once and processed often 

    -   HPC systems may not scale well to such massive datasets being uploaded. 

## Apache Spark

Fast, expressive cluster computing system compatible with Apache Hadoop 

-   It is much **faster** and much **easier** than Hadoop MapReduce to use due its rich APIs 
-   Large community 
-   Goes far beyond batch applications to support a variety of workloads:
    -   including interactive queries, streaming, machine learning, and graph processing 

General-purpose cluster in-memory computing system 

The **key concept** in Spark are datasets called **RDD**s (**R**esilient **D**istributed **D**ataset ) 

-    load data into RDDs and perform some **operations** 

Once created, RDDs offer two types of operations:

-   transformations

    -   transformations include **map**, **filter**, **join**
    -   **[lazy](https://stackoverflow.com/questions/38027877/spark-transformation-why-its-lazy-and-what-is-the-advantage/39438038#39438038?newreg=abd4601d30b14c318a66bb16918c1110)** operation to build RDDs from other RDDs

-   actions

    -   actions include **count**, **collect**, **save** 

    -   return a result or write it to storage

### When to use

Spark’s in-memory capabilities are not the best fit for all use cases: 

-   For many **simple** use cases Apache MapReduce and Hive might be a more appropriate choice 
-   Spark was **not** designed as a **multi**-user environment 
-   Spark users are required to know that **memory** they have is sufficient for a dataset 
-   Adding more users adds complications, since the users will have to coordinate memory usage to run code 

# Data streaming

## ML techniques

-   Online learning 
    -   Data becomes available sequentially
    -   Model is updated continuously 
    -   Data is discard after use
    -   Not for multiple passes: cluster, k-means
    -   Works for single pass: Naïve 👓️ Bayes
-   Offline learning
-   Sequential access 
-   Random access 

# Blockchain

Currently two types of blockchains 

- Public blockchains (e.g., Bitcoin, Ethereum) 
- Private blockchains (e.g., business blockchains produced by Hyperledger Fabric) 

## What

A distributed Ledger 

- The system of record for a business

- Stores a list of transactions

- Shared with network peers 

## Good use case

-   Business problem to be solved
-   An identifiable business network
-   A need for **Trust** 
------
- Asset trading
     - Stocks, Shares, Property, Music, Energy
    - Directly selling time-shares like taxi, rooms, office space 

- Supply chain management
- Autonomous execution of business contracts
- Asset provenance 

## Hyperledger Fabric 

- Useful for **business** networks, e.g., 
     - Supply chain management
    - Assets trading 

- Supports Smart Contracts
     - Chain code provide general application capabilities 

- Platform services based on Fabric already exist 
     - E.g., Oracle blockchain platform 

- Still relatively new
    	- but already many business users 