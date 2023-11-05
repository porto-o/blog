# Introduction

To begin with, let's justify why SQL and XML can have a really good match.
## Why XML?

XML is a technology that **allows an efficient data exchange on the web**, therefore, when we are talking about web applications and data storage, XML databases might be a good choice.

Moreover, its **simplicity and extensibility** make XML a very comfortable format to work with, due to this, many companies have supported this technology through out the years.
## However...

* Queries to retrieve data from XML documents might get a little complicated because of the **unstructured model**.

* The administration and update of XML documents can get complicated and really tedious.

# Native XML Databases

This type of databases are quite special since it has **define a logic model for XML documents**, this is, a model that allows us to **retrieve and store** documents.

Furthermore, native xml databases must have support for the following tools:

1. Elements
2. Attributes
3. PCDATA

On the other side, this type of databases are not required to offer any particular model for physical storage, i.e. the database can be **on top of a relational, hierarchy or Object Oriented databases**.
## Characteristics
* Define logic models for XML
	* They **map the models to the corresponded storage mechanism**.
	* The operations with the documents are made on XML
	* They offer **a high level of abstraction**.
	* **Schema dependency**
		* The documents are ==data collections==.
		* The ==schema is not necessary for **storing data**==
		* The schemas are defined with [[XML Schema|DTD or XML Schemas]]
	* They do not use an **specific mechanism of physical storage**.
		* Depends on each product (Oracle, Microsoft...)
	* The **basic unit of storage is an XML document**
## Benefits
1. Not only do xml documents can be stored but also stylesheets.
2. The data model is flexible and simple.
3. High performance.
4. Complement RDBMS with mapping for XML.
## Solutions
| Natives | On top of an OODB | On top of a Relational DB |
| --- | --- | --- |
| eXist-db | ozone | DB2 (IBM) |
| MarkLogic | --- | Oracle |
| OpenLink Virtuoso | --- | PostgreSQL |

# SQL + XML standard

One of the problems with XML was that each manufacturer developed tools to manipulated them, therefore there were tons of problems when looking implement XML in our databases.
To solve this, ISO defined a new standard to **create and manipulate XML documents**.

> [ISO/IEC 9075-14: XML-Related Specifications (SQL/XML)](https://www.iso.org/standard/76587.html)

* New **predefined type**.
* New **operators to create and manipulate _values_ of XML type**.
* Rules to map tables, schemas and catalogues to XML.
# RDBMS and XML

At the end of the day XML documents are just plain text, therefore we might think that the way to store XML documents in database should be in LOB, VARCHAR or nested tables.
However, this is **not efficient nor comfortable to work with**.

>[!Example] Example
>Imagine you want to get the value of an element that is almost at the end of your DOM, if we had the value as plain text in fields of VARCHAR type, we would need to filter the text through one of the vast amount of programming languages.
>This is a very stressful and complex way to get the value.

Therefore, **special data type** is needed to store these XML documents. This is the alternative that almost every management systems use (Oracle, PostgreSQL, DB2,...)

# XML data type

One of the advantages of using special XML data type is that it allows to store XML documents in a native way. Moreover, it can be represented as XML documents indeed, not as plain text.

This data type allows to store:

1. Well formed XML documents
2. XML Body
3. It is **based in XQuery**. The value of a XML data type is an **instance of a XQuery model**.

## Support for XML data type

* Oracle and IBM implement SQL/XML
* Microsoft support similar features but with proprietary syntax.
* All of the support XQuery in SQL.
* **Differences in the physical implementation**.
	* Oracle 10g uses CLOB and OR tables
	* Microsoft 2005 and 2008 uses BLOB with proprietary format.
	* DB2 V9 uses CLOB
![[Pasted image 20231021191010.png]]