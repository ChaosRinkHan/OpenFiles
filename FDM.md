<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Data formats](#data-formats)
  - [Data format](#data-format)
    - [HDF5](#hdf5)
      - [Parallel HDF5](#parallel-hdf5)
    - [netCDF](#netcdf)
      - [CDL (Common Data Language)](#cdl-common-data-language)
      - [High-performance NetCDF](#high-performance-netcdf)
        - [Enhanced NetCDF (version 4 and beyond)](#enhanced-netcdf-version-4-and-beyond)
      - [PNetCDF](#pnetcdf)
    - [What to use](#what-to-use)
  - [I/O](#io)
  - [Lustre](#lustre)
  - [File system](#file-system)
  - [XML & JSON](#xml--json)
    - [XML](#xml)
      - [WSDL](#wsdl)
      - [SOAP](#soap)
      - [Validation: XML schemas](#validation-xml-schemas)
      - [Phasers](#phasers)
    - [JSON](#json)
      - [Validation](#validation)
  - [Metadata](#metadata)
    - [why](#why)
    - [Good metadata](#good-metadata)
    - [System Metadata / Structural Metadata](#system-metadata--structural-metadata)
    - [Content Metadata / Descriptive Metadata](#content-metadata--descriptive-metadata)
    - [Create](#create)
    - [Standards](#standards)
    - [Semantics](#semantics)
    - [Ontology](#ontology)
    - [Summary](#summary)
  - [Persistent Identifiers PID](#persistent-identifiers-pid)
    - [why](#why-1)
    - [what](#what)
    - [PIDs identify:](#pids-identify)
    - [Characteristics](#characteristics)
    - [Advantages](#advantages)
    - [Disadvantages](#disadvantages)
- [Database](#database)
  - [Relational Databases](#relational-databases)
    - [ER (entity relationship) diagram](#er-entity-relationship-diagram)
  - [NoSQL Databases](#nosql-databases)
    - [Mongo DB](#mongo-db)
      - [Normalised Model](#normalised-model)
      - [De-normalised Model](#de-normalised-model)
  - [RDF Database](#rdf-database)
- [Semantic data](#semantic-data)
  - [SPARQL](#sparql)
- [Data lifecycle, DMP](#data-lifecycle-dmp)
  - [Components](#components)
  - [Data management planning](#data-management-planning)
    - [What](#what)
    - [Why](#why)
    - [Components](#components-1)
- [Law](#law)
  - [GDPR](#gdpr)
- [Archiving and preservation](#archiving-and-preservation)
  - [OAIS](#oais)
- [Data infrastructure and hardware](#data-infrastructure-and-hardware)
    - [Durability](#durability)
  - [Storage architecture](#storage-architecture)
- [MapReduce](#mapreduce)
  - [Map](#map)
  - [Process](#process)
- [Hadoop](#hadoop)
  - [vs MPI/HPC• Fault tolerance](#vs-mpihpc%E2%80%A2-fault-tolerance)
  - [Apache Spark](#apache-spark)
    - [When to use](#when-to-use)
- [Blockchain](#blockchain)
  - [What](#what-1)
  - [Good use case](#good-use-case)
  - [Hyperledger Fabric](#hyperledger-fabric)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Data formats 

Digital data: encoding, file format, files, records

-   Encoding: interpreting groups of bits 

-   Endian: big, little 
-   Unicode, UTF

-   Format: interpreting decoded bit-groups (bytes, characters) 

-   File: basic unit of data organisation. Pointer, metadata.
-   Files vs objects
    -   Object storage is becoming more **common** – especially in “big data” contexts, match with http/REST model of resources on the Web 
    -   Metadata: 
        -   File: central location using fixed schema, scalability becomes an issue
        -   Objects: metadata bundled with content with flexible schema, scalability much better 

|             | File                                          | Objects                                   |
| ----------- | --------------------------------------------- | ----------------------------------------- |
| Metadata    | stored in central location using fixed schema | bundled with content with flexible schema |
| Findability | straightforward (read the inode table)        | can be a challenge                        |
| Scalability | becomes an issue                              | much better                               |

## Data format

### HDF5

**Hierarchical Data Format (version 5)**

Binary but portable

>   *HDF5 is a unique technology suite that makes possible the management of extremely large and complex data collections.* 

-   <!--A versatile **data model** that can represent very complex data objects and a wide variety of metadata.--> 
-   <!--A completely **portable file format** with no limit on the number or size of data objects in the collection.--> 
-   <!--A **software library that** runs on a range of computational platforms--> 

-   <!--A rich set of integrated **performance** features that allow for access time and storage space optimizations.--> 
-   <!--Tools and applications for managing, manipulating, viewing, and analyzing the data in the collection.--> 

-   Based on *groups* and *datasets*
    -   Structure
    -   Portability
    -   Performance
    -   Free & Open Source
-   Group: header, symbol label
-   Datasets: header, data array

#### Parallel HDF5 





-   CDF. Binary and portable 

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

### why

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

### why

Reliably refer to a particular piece of data.

Objects need to be (globally) addressable so that they can be reusable.

Once data is addressable, it can be 

-   found more easily by you, other people, and computers – can be 
-   cited
-   linked together 

### what

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

## Relational Databases 

### ER (entity relationship) diagram

-   Produces a data model representing a real-world situation 
    -   Identifies important entities (tables)
    -   Relationship between the entities. 

-   Allows simplification of the data model
    -   E.g., Remove many-to-many relationships 
-   Cardinality: 1-1. 1-m, m-1, m-n

## NoSQL Databases

No schemas are required 

No join operations 

No ACID transactions 

### Mongo DB

Open Source JSON-**like** document based database management system 

-   High performance
-   High availability

Documents contains collections of key-value pairs

4 basic CRUD operations: create, read, update, delete

#### Normalised Model

Pros:

-   No duplication of data 

Cons: 

-   Requires several request for an update. First get the references. Then get the documents refer to by the references. And then update those documents 

#### De-normalised Model

Pros: 

-   Single document contains all interested data
-   Can be updated with single request 

Cons:

-   Data duplication can occur 
-   If necessary, application would need to manage potential data duplication 

## RDF Database

# Semantic data

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
    -   The data lifecycle maps well onto a typical research or experiment timeline 
    -   Planned and effective DM is becoming a feature of modern research 
-   Product data management
-   Test data management

## Components

Plan -> acquire -> assure -> describe -> preserve -> discover -> combine -> process -> plan -> ...

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
-   Increasingly, compulsory!
     – research funding agencies now ask for DMPs for most proposals 

### Components

1.  Information about data & data formats
2.  Metadata content and format
3.  Policies for access, sharing and re-use
4.  Long-term storage and data management 
5.  Budget 

# Law

## GDPR

 General Data Protection Regulation 

-   codifies & harmonises data subject rights 

# Archiving and preservation

## OAIS

Open Archival Information System reference model 

![image-20191214111943930](https://i.imgur.com/XdNlAqU.png)

-   Designed for central, long-term archives
    -   Long term
    -   Designated Community
    -   Representation Information (RI): 

# Data infrastructure and hardware

-   Amdahl number

    IO bandwidth (bits/s) / CPU clock rate = 1 (ideally)

-   Amdahl memory ratio

    memory size (bytes) / instructions per second = 1 (ideally) 

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

A function is “mapped” over all of the input data. Return a list of (key, value) pairs

-   When you do MapReduce at scale, the Map function is run on every node where the input data resides 

## Process

![image-20191214161344941](https://i.imgur.com/z3oe3hW.png)

# Hadoop

Distributed File System + Map Reduce Framework + Supporting Functionality 

Each Hadoop job reads data from the HDFS and writes output to the HDFS 

-   Fine for short chains of processing 
-   Very inefficient for iterative algorithms
-   Spark – supports caching data 
-   Twister – iterative map reduce 

## vs MPI/HPC• Fault tolerance 

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

-   It is much faster and much easier than Hadoop MapReduce to use due its rich APIs 
-   Large community 
-   Goes far beyond batch applications to support a variety of workloads:
    -   including interactive queries, streaming, machine learning, and graph processing 

General-purpose cluster in-memory computing system 

The **key concept** in Spark are datasets called **RDD**s (**R**esilient **D**istributed Dateset ) 

-    load data into RDDs and perform some **operations** 

Once created, RDDs offer two types of operations:

-   transformations

    -   transformations include map, filter, join
    -   lazy operation to build RDDs from other RDDs

-   actions

    -   actions include count, collect, save 

    -   return a result or write it to storage

### When to use

Spark’s in-memory capabilities are not the best fit for all use cases: 

-   For many simple use cases Apache MapReduce and Hive might be a more appropriate choice 
-   Spark was not designed as a multi-user environment 
-   Spark users are required to know that memory they have is sufficient for a dataset 
-   Adding more users adds complications, since the users will have to coordinate memory usage to run code 

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



- Asset trading
     - Stocks, Shares, Property, Music, Energy
    - Directly selling time-shares like taxi, rooms, office space 

- Supply chain management
- Autonomous execution of business contracts
- Asset provenance 

## Hyperledger Fabric 

- Useful for business networks, e.g., 
     - Supply chain management
    - Assets trading 

- Supports Smart Contracts
     - Chain code provide general application capabilities 

- Platform services based on Fabric already exist 
     - E.g., Oracle blockchain platform 

- Still relatively new
    	- but already many business users 