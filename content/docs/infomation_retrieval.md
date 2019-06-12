---
title: "Infomation_retrieval"
date: 2019-05-19T21:29:03-07:00
draft: true
---

Slides: http://lintool.github.io/UMD-courses/LBSC796-INFM718R-2006-Spring/lecture1.pdf

https://www.slideshare.net/WebST_IBA/information-retrieval-9353486

---

# [Information Retrieval Systems](https://en.wikipedia.org/wiki/Information_retrieval)

Information retrieval (IR) is the activity of obtaining information system resources relevant to an information need from a collection. Searches can be based on full-text or other content-based indexing. Information retrieval is the science of searching for information in a document, searching for documents themselves, and also searching for metadata that describe data, and for databases of texts, images or sounds.

Automated information retrieval systems are used to reduce what has been called information overload. An IR system is a software that provide access to books, journals and other documents, stores them and manages the document. Web search engines are the most visible IR applications.

---

An information retrieval process begins when a user enters a query into the system. Queries are formal statements of information needs, for example search strings in web search engines. In information retrieval a query does not uniquely identify a single object in the collection. Instead, several objects may match the query, perhaps with different degrees of relevancy.

An object is an entity that is represented by information in a content collection or database. User queries are matched against the database information. However, as opposed to classical SQL queries of a database, in information retrieval the results returned may or may not match the query, so results are typically ranked. This ranking of results is a key difference of information retrieval searching compared to database searching.

Depending on the application the data objects may be, for example, text documents, images, audio, mind maps or videos. Often the documents themselves are not kept or stored directly in the IR system, but are instead represented in the system by document surrogates or metadata.

Most IR systems compute a numeric score on how well each object in the database matches the query, and rank the objects according to this value. The top ranking objects are then shown to the user. The process may then be iterated if the user wishes to refine the query.

---

https://www.sciencedirect.com/topics/computer-science/information-retrieval-systemshttps://www.sciencedirect.com/topics/computer-science/information-retrieval-systems

### Information Retrieval System
The information retrieval system is also made up of two components: the indexing system and the query system. The first of these is in charge of analyzing the documents downloaded from the Web and with the creating of indexes that then allow search queries to be made; while the second is the search engine’s visible interface, that is, the part with which users interact.

If a search engine is able to answer questions in such astonishingly short spaces of time as we have become accustomed to (typically, fractions of a second), it is because they do not explore the Web for users in real time (that is, as and when the query is made), but rather they use an index that is updated regularly (several times a day).

A system that attempted to explore the documents on the Web sequentially and in real-time to provide answers would not make the slightest bit of sense. Days or even weeks could pass between the question being asked and an answer being given. Instead of this, what a search engine does is to query its internal indexes.


### Indexing
Most information retrieval systems, whether online or manual, are based on some form of indexing. The library catalogue is really a kind of index, albeit often a rather sophisticated one. It refers the user to particular shelf numbers (those numbers used to place and locate books and other physical information resources on the shelves) or to particular files on the world wide web. Similarly, an index at the back of a book refers the reader to page numbers.

Other indexing systems refer not to physically whole items nor to single pages, but to a series of pages that comprise a particular article – they index articles from journals and other forms of serial publication. Nowadays, most of these systems are online, and many constitute very large databases covering hundreds or thousands of serials; many also provide links to online versions of some of the articles they index. Along with the usual types of bibliographic element such as title, author’s name, subject descriptors, many systems include abstracts, or short summaries, of some or all of the articles indexed. Hence these systems are often referred to as indexing and abstracting services. Prominent examples include MEDLINE, LexisNexis, Chemical Abstracts and LISTA (Library, Information Science & Technology Abstracts) – see Chapter 7.

Many libraries and information resource centres provide access to a range of these services as they also house (either physically or virtually) many of the corresponding serials. Conventionally, the databases are not integrated with the library catalogue, but increasingly libraries are offering users a federated search facility. This allows them to search on multiple databases, including the library catalogue, simultaneously. Nevertheless, the bibliographic data are still stored in separate databases. There are several reasons for this. First, most indexing and abstracting services are commercial concerns – their proprietors need to keep control of the (meta)data. Second, users may wish to limit their search to one particular database with one particular kind of resource. Third, the indexing performed varies across databases, so that different databases use different subject terms, and include different bibliographic elements, according to the nature of material being indexed. Library catalogues are based on standards such as the Anglo-American Cataloguing Rules (see the following section) but these are usually not applied by indexing and abstracting services.

Although the product of any index is metadata, this does not mean that all metadata are indexed (and therefore used as access points). Some types of information may be deemed worth recording, but not considered to be what users would normally search on – such as the number of pages a book has. Thus, library cataloguing distinguishes between description and indexing. Bibliographic description is set out in a particular way to be read, once the record has been retrieved via the index. Not all of this description would necessarily be indexed, indeed, most will usually not be, but users may want to read it, in order to select or deselect an item – they may be interested in how long a book is or when it was published, for instance.

It may also be that the information is represented in a way that makes it less appropriate for indexing, for instance, it may be in whole sentences rather than a few key terms. Nowadays, many IR systems can retrieve on any word (or number), but this does not mean that everything should be indexed. Words such as ‘a’ and ‘the’ are too common, as well as almost meaningless, to be of much use, and are often not indexed (these are referred to as stop words). The fewer terms indexed, the more likely it is the system will retrieve relevant documents (and less irrelevant ones). The more terms indexed the more likely it is that the system will retrieve more documents that are relevant, but also more irrelevant ones. This brings up a key issue in indexing – vocabulary control.

---

http://www.doc.ic.ac.uk/~nd/surprise_97/journal/vol2/hks/infor_ret.html

### Information Retrieval & Search Algorithms

Information retrieval is the task, given a set of documents and a user query, of finding the relevant documents. Information retrieval applications require speed, consistency, accuracy and ease of use in retrieving relevant texts to satisfy user queries. These evaluation criteria apply to other text interpretation applications as well.

**Accuracy**: The sheer volumes of information now stored in electronic media magnify deficiencies in recall (the percentage of relevant information retrieved. Giving the user reasonable-sized response with high precision can mean missing hundreds of relevant texts.

**Speed** : As the quantity of text that must be searched increases, the speed of searching can become a reserve bottleneck. In practical terms, the need for fast search means that more computational-intensive processing such as NLP techniques must either apply very selectively or run as "batch" indexing tool prior to retrieval.

**Consistency** : Many information retrieval environments require indexing of the text by the groups of indexers or by the authors. This leads to a decrease in accuracy from the inevitable inconsistencies, which automatic processing could help to avoid.

**Ease of use** : The growth of personal computer has mode obsolete the traditional model of information retrieval with a trained human intermediary, giving systems responsiveness a high priority.
NetOwl By IsoQuest NetOwl is a family of information retrieval and data extraction software developed by IsoQuest cooperation. This software uses latest and most advanced Natural Language Processing Technology. Some of the members of this software family are as follows.

+ Desktop
+ Datablade
+ Intelligence Server
+ Extender
+ Discovery Suite
+ Extractor

**Search Algorithms** : Virtually all AI applications use some sort of searching to find the desired solutions. Therefore study and research of search algorithms is very important for the development of AI based systems including natural language processing.

---

https://www8.cs.umu.se/kurser/TDBC86/H06/Slides/1_OH_intro.pdf

### Three types of information systems:
#### Information-Retrieval Systems (IR)
+ Search large bodies of information which are not
specifically formatted as formal data bases.
+ Web search engine
+ Keyword search of a text base
+ Typically read-only
#### Database Management Systems (DBMS)
+ Relatively small schema
+ Large body of homogeneous data
+ Minor or no deductive capability
+ Extensive formal update capability
+ Shared use for both read and write
#### Knowledge-Base Systems (KBS)
+ Relatively small body of heterogeneous information
+ Significant deductive capability
+ Typical use: support of an intelligent application.

---

https://nlp.stanford.edu/IR-book/pdf/01bool.pdf

---

http://dns.uls.cl/~ej/daa_08/Algoritmos/books/book5/chap01.htm

---



