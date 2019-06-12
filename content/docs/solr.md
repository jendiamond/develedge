---
title: "Solr"
date: 2019-05-19T21:30:34-07:00
draft: true
---

<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UPApache Solr is an Open-source REST-API based Enterprise Real-time Search and Analytics Engine Server from Apache Software Foundation. It’s core Search Functionality is built using Apache Lucene Framework and added with some extra and useful features. It is written in Java Language.

SOLR stands for Searching On Lucene w/Replication. It’s main functionalities are indexing and serching. Like ElasticSearch, it is also a Document-based NoSQL Data Store.</summary>

</details>

>#### [Solr Query Language Cheat Sheet](https://doc.lucidworks.com/fusion/3.1/Search/Query-Language-Cheat-Sheet.html)  
>**q** - Query parameters. The full Solr query, using Lucene query syntax.
>
>**fq** - Filter query. A query string that limits the query results without influencing their scores.
>
>**sort** - Sort field/direction. The field on which to sort, followed by a space and direction (desc or asc). You can specify multiple sort fields like this: sort=title asc,year desc
>
>**rows** - Max results per page. This set the "page size" for paginated search results.
>
>**start** - Pagination offset. The number of results to skip, for pagination purposes.
>
>**fl** - Field List. The list of fields to return in the query results.
>
>**df** - Default field. Used to configure the q and fq parameters. If not specified, the default field is text.
>
>**wt** - Response writer. Select the response format by specifying one of Solr’s response writers.
> ##### Wildcards
>**?** – Single-character wildcard
>
><b>*</b> – Multi-character wildcard


From Val - https://wiki.apache.org/solr/CommonQueryParameters

Benefits of Apache Solr:-

+ It is open-source
It has very useful Administrative Interface.
+ Light Weight with REST API
+ It is very fast, simple, powerful and flexible search engine
+ Unlike ElasticSearch, it supports not only JSON format, other useful formats too: XML, PHP, Ruby, Python, XSLT, Velocity and custom Java binary output formats over HTTP.
+ Highly Available. Easy and Highly Scalable. Robust, fault tolerant and reliable search engine.
+ Schema free data store. However, if required we can create a schema to support our data.
+ Fast Search Performance because of Apache Lucene Inverted Index.
+ Supports both Structured and UN-Structured Data
+ Supports Distributed, Sharding, Replication, Clustering and Multi-Node Architecture
+ Supports Bulk Operations
+ Easily Extendable with new plugins
+ Supports Caching Data
+ Useful for BigData Environments
+ Unlike ElasticSearch, it supports MapReduce algorithm

#### Videos
+ [Our SOLR](http://localhost:8983/solr/)
+ [Query Screen](https://lucene.apache.org/solr/guide/6_6/query-screen.html)
+ [SimpleFacetParameters](https://wiki.apache.org/solr/SimpleFacetParameters)
+ [Solr in 5 Minutes - Ignite Style Presentation](https://www.youtube.com/watch?v=ClhrrPzJWmI)
+ [Solr Basics - solr script, Solr Admin, directories and examples](https://www.youtube.com/watch?v=LhN_y1knuVs)
+ [Solr Indexing Sample Docs to solr core and searching with various filter query options](https://www.youtube.com/watch?v=rxoS1p1TaFY)
+ [SolrTutorial.com](http://www.solrtutorial.com)
+ [Solr n' Stuff](http://yonik.com/solr/query-syntax/)
+ [Apache Solr Hello World Example](https://www.mkyong.com/solr/apache-solr-hello-world-example/)
