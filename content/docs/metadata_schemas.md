---
title: "Metadata Schemas & Serialization"
date: 2019-05-19T21:29:33-07:00
draft: true
---

### Dublin Core | MARC | RDF | JSON-LD | XML

---

## Dublin Core
<details><summary>The Dublin Core Schema is a small set of vocabulary terms that can be used to describe digital resources (video, images, web pages, etc.), as well as physical resources such as books or CDs, and objects like artworks.</summary>

Dublin Core is an initiative to create a digital "library card catalog" for the Web. Dublin Core is made up of 15 metadata (data that describes data) elements that offer expanded cataloging information and improved document indexing for search engine programs.

### The 15 metadata elements used by Dublin Core are: 
1. title - the name given the resource
1. creator - the person or organization responsible for the content
1. subject - the topic covered
1. description - a textual outline of the content
1. publisher - those responsible for making the resource available
1. contributor - those who added to the content
1. date - when the resource was made available
1. type - a category for the content
1. format - how the resource is presented
1. identifier - numerical identifier for the content such as a URL
1. source - where the content originally derived from
1. language - in what language the content is written
1. relation - how the content relates to other resources, for instance, if it is a chapter in a book
1. coverage - where the resource is physically located
1. rights - a link to a copyright notice

### Two forms of Dublin Core exist: 
1. Simple Dublin Core and Qualified Dublin Core.
Simple Dublin Core expresses elements as attribute-value pairs using just the 15 metadata elements from the Dublin Core Metadata Element Set. 
2. Qualified Dublin Core increases the specificity of metadata by adding information about encoding schemes, enumerated lists of values, or other processing clues. While enabling searches to be more specific, qualifiers are also more complex and can pose challenges to interoperability.

Each method of recording or transferring Dublin Core metadata has its plusses and minuses. HTML, XML, RDF, and relational databases are among the more common methods.

The Dublin Core Metadata Initiative began in 1995, taking its name from the location of the original workshop, Dublin, Ohio. It has since become international in scope and has representatives from more than 20 countries now contributing. Dublin Core has always held that resource discovery should be independent from the medium of the resource. So, while Dublin Core targets electronic resources, it aims to be flexible enough to help in searches for more traditional formats of data too. Web sites, though, are the most common users of Dublin Core.

#### [Metadata Basics](http://dublincore.org/resources/metadata-basics/)
#### [DCMI Metadata Terms](http://www.dublincore.org/specifications/dublin-core/dcmi-terms/)

</details>

---

## MARC
<details><summary>**MARC (MAchine-Readable Cataloging)** standards are a set of digital formats for the description of items catalogued by libraries, such as books. Working with the Library of Congress, American computer scientist Henriette Avram developed MARC in the 1960s to create records that could be read by computers and shared among libraries.</summary>

http://www.librarian.net/talks/marcmetadata/#two

https://en.wikipedia.org/wiki/MARC_standards  
**MARC (MAchine-Readable Cataloging)** standards are a set of digital formats for the description of items catalogued by libraries, such as books. Working with the Library of Congress, American computer scientist Henriette Avram developed MARC in the 1960s to create records that could be read by computers and shared among libraries.

By 1971, MARC formats had become the US national standard for dissemination of bibliographic data. Two years later, they became the international standard. There are several versions of MARC in use around the world, the most predominant being MARC 21, created in 1999 as a result of the harmonization of U.S. and Canadian MARC formats, and UNIMARC, widely used in Europe. The MARC 21 family of standards now includes formats for authority records, holdings records, classification schedules, and community information, in addition to the format for bibliographic records.

#### MARC 21
MARC 21 was designed to redefine the original MARC record format for the 21st century and to make it more accessible to the international community. MARC 21 has formats for the following five types of data: Bibliographic Format, Authority Format, Holdings Format, Community Format, and Classification Data Format.[2] Currently MARC 21 has been implemented successfully by The British Library, the European Institutions and the major library institutions in the United States, and Canada.

MARC 21 is a result of the combination of the United States and Canadian MARC formats (USMARC and CAN/MARC). MARC21 is based on the NISO/ANSI standard Z39.2, which allows users of different software products to communicate with each other and to exchange data.

MARC 21 allows the use of two character sets, either MARC-8 or Unicode encoded as UTF-8. MARC-8 is based on ISO 2022 and allows the use of Hebrew, Cyrillic, Arabic, Greek, and East Asian scripts. MARC 21 in UTF-8 format allows all the languages supported by Unicode.

#### [A Very Brief Review of
the MARC 21 Bibliographic Format](http://web.simmons.edu/~joudrey/marc/)

The MARC (MAchine-Readable Cataloging) encoding system has been used to create electronic catalog records since the mid-1960s. The most current version for use in the United States is MARC 21, a harmonized version of USMARC and CAN/MARC, first published in 1999 and continually revised. Currently, the MARC encoding system holds the position of being the one used for bibliographic records in the vast majority of the world’s online catalogs, although this is poised for change.

##### MARC21 consists of five specific formats:

+ **Bibliographic format**: for encoding bibliographic data in records that are surrogates for information resources
+ **Authority format**: for encoding authority data collected in authority records created to help control the content of those surrogate record fields that are subject to authority control
+ **Holdings format**: for encoding data elements in holdings records that show the holdings and location data for information resources described in surrogate records
+ **Community information format**: for encoding data in records that contain information about events, programs, services, and the like
+ **Classification data format**: for encoding data elements related to classification numbers, the captions associated with them, their hierarchies, and the subject headings with which they correlate

Each MARC format is made up of three structural elements: 
+ the record structure
+ the content designation
+ the actual metadata content

**Record structure** refers to MARC's implementation of the Format for Information Exchange (ISO 2709) and Bibliographic Information Interchange (ANSI/NISO Z39.2), which address the technical aspects of the MARC standard.

**Content designation** refers to semantics. It addresses the use of tags and subfield codes to specifically identify and label the metadata held in parts of MARC records. Content designation allows automated library systems to process, index, and manipulate the data found in the record as needed.

**Content** refers to the metadata contained in the record, formatted according to content standards, controlled vocabularies, classification schemes, and the like.


#### Videos
+ [Beyond MARC: Metadata Standards for Digital Resources](https://www.youtube.com/watch?v=ozKg08td5mE)
+ [What is a MARC record?](https://www.youtube.com/watch?v=fdwF2Jf-RsY)
+ [basics of metadata](https://www.youtube.com/watch?time_continue=6&v=-0vc6LeVa14)
+ [MARC 21](https://www.youtube.com/watch?v=-92mEmB6wa8)

</details>

---

## [RDF](https://www.w3.org/RDF/)
<details><summary>Resource Description Framework was originally designed as a metadata data model. It has come to be used as a general method for conceptual description or modeling of information that is implemented in web resources, using a variety of syntax notations and data serialization formats.</summary>

It is based on the idea of making statements about resources in expressions of the form subject–predicate–object, known as triples.

The **subject** denotes the resource,   
and the **predicate** denotes traits or aspects of the resource,  
and expresses a relationship between the subject and the object.

For example, one way to represent the notion  
"The sky has the color blue" in RDF is as the triple:  
a subject denoting **"the sky"**,  
a predicate denoting **"has the color"**,  
and an object denoting **"blue"**.  
Therefore, RDF uses subject instead of object (or entity) in contrast to the typical approach of an entity–attribute–value model in object-oriented design:  
entity (sky),  
attribute (color),  
and value (blue).

RDF's simple data model and ability to model disparate, abstract concepts has also led to its increasing use in knowledge management applications unrelated to Semantic Web activity.

RDF data is often stored in relational database or native representations (also called Triplestores—or Quad stores, if context such as the named graph is also stored for each RDF triple).

### [RDF::URI.intern](https://www.rubydoc.info/github/ruby-rdf/rdf/RDF%2FURI.intern)
`.intern(str, *args) ⇒ RDF::URI`  
Returns an interned `RDF::URI` instance based on the given uri string.

The maximum number of cached interned URI references is given by the `CACHE_SIZE` constant. This value is unlimited by default, in which case an interned URI object will be purged only when the last strong reference to it is garbage collected (i.e., when its finalizer runs).

Excepting special memory-limited circumstances, it should always be safe and preferred to construct new URI references using `RDF::URI.intern` instead of `RDF::URI.new`, since if an interned object can't be returned for some reason, this method will fall back to returning a freshly-allocated one.

(see #initialize)

Returns: `(RDF::URI)` — an immutable, frozen URI object

#### Videos
+ [RDF Tutorial - An Introduction to the Resource Description Framework](https://www.youtube.com/watch?v=zeYfT1cNKQg)
+ [Semantic Web Tutorial 3/14: Resource Description Framework (RDF) 1/2](https://www.youtube.com/watch?v=6geSpcUJjBA)
+ [KOMMA: Modeling with RDF and linked data](https://www.youtube.com/watch?v=bYQa8fbsjeg)

</details>

---

## [JSON-LD](https://json-ld.org/)
<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UP</summary>
#### Videos
+ [What is JSON-LD?](https://www.youtube.com/watch?v=vioCbTo3C-4)
+ [Understanding JSON-LD Structured Data](https://www.youtube.com/watch?v=MF9lS3UU0ww)
+ [JSON-LD: Core Markup](https://www.youtube.com/watch?v=UmvWk_TQ30A)

JavaScript Object Notation for Linked Data, is a method of encoding Linked Data using JSON. It was a goal to require as little effort as possible from developers to transform their existing JSON to JSON-LD. This allows data to be serialized in a way that is similar to traditional JSON.

```
{
  "@context": {
    "name": "http://xmlns.com/foaf/0.1/name",
    "homepage": {
      "@id": "http://xmlns.com/foaf/0.1/workplaceHomepage",
      "@type": "@id"
    },
    "Person": "http://xmlns.com/foaf/0.1/Person"
  },
  "@id": "https://me.example.com",
  "@type": "Person",
  "name": "John Smith",
  "homepage": "https://www.example.com/"
}
```

[A Guide to JSON-LD for Beginners](https://moz.com/blog/json-ld-for-beginners)

</details>

---

## XML
<details><summary>FOLLOW THESE DIRECTIONS TO GET IT SET UP</summary>
#### Videos
+ [XML Tutorial for Beginners Theory - YouTube](https://www.youtube.com/watch?v=n-y-YHVZSwk)
+ [An Introduction to XML: The Basics Part 1](https://www.youtube.com/watch?v=Q0k5ySZGPBc)
+ [Organization & Representation of Information](http://eduscapes.com/digital/4.htm)

XML stands for eXtensible Markup Language. XML is a markup language much like HTML. XML was designed to store and transport data. XML was designed to be self-descriptive. XML is a W3C Recommendation.

### Key terminology
The material in this section is based on the XML Specification. This is not an exhaustive list of all the constructs that appear in XML; it provides an introduction to the key constructs most often encountered in day-to-day use.

#### Character
An XML document is a string of characters. Almost every legal Unicode character may appear in an XML document.
Processor and application
The processor analyzes the markup and passes structured information to an application. The specification places requirements on what an XML processor must do and not do, but the application is outside its scope. The processor (as the specification calls it) is often referred to colloquially as an XML parser.

#### Markup and content
The characters making up an XML document are divided into markup and content, which may be distinguished by the application of simple syntactic rules. Generally, strings that constitute markup either begin with the character < and end with a >, or they begin with the character & and end with a ;. Strings of characters that are not markup are content. However, in a CDATA section, the delimiters <![CDATA[ and ]]> are classified as markup, while the text between them is classified as content. In addition, whitespace before and after the outermost element is classified as markup.

#### Tag
A tag is a markup construct that begins with < and ends with >. Tags come in three flavors:
start-tag, such as <section>;
end-tag, such as </section>;
empty-element tag, such as <line-break />.

#### Element
An element is a logical document component that either begins with a start-tag and ends with a matching end-tag or consists only of an empty-element tag. The characters between the start-tag and end-tag, if any, are the element's content, and may contain markup, including other elements, which are called child elements. An example is <greeting>Hello, world!</greeting>. Another is <line-break />.

#### Attribute
An attribute is a markup construct consisting of a name–value pair that exists within a start-tag or empty-element tag. An example is <img src="madonna.jpg" alt="Madonna" />, where the names of the attributes are "src" and "alt", and their values are "madonna.jpg" and "Madonna" respectively. Another example is <step number="3">Connect A to B.</step>, where the name of the attribute is "number" and its value is "3". An XML attribute can only have a single value and each attribute can appear at most once on each element. In the common situation where a list of multiple values is desired, this must be done by encoding the list into a well-formed XML attribute[i] with some format beyond what XML defines itself. Usually this is either a comma or semi-colon delimited list or, if the individual values are known not to contain spaces,[ii] a space-delimited list can be used. <div class="inner greeting-box">Welcome!</div>, where the attribute "class" has both the value "inner greeting-box" and also indicates the two CSS class names "inner" and "greeting-box".

#### XML declaration
XML documents may begin with an XML declaration that describes some information about themselves. An example is <?xml version="1.0" encoding="UTF-8"?>.

</details>
