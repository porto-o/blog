# What is XML?
XML is a universal metalanguage to define labels. It offers a uniform workflow to exchange data or metadata among applications.

XML files offers a **hierarchy data format**, i.e. each label might have _children labels_ so at the end of the day we will have a **[[XML DOM|tree of labels]]**.

However, XML does not offer any help to know about the semantic of our data, for example:

```XML
<name>Pablo</name>

<!--The element 'name' might refer to the name of a person, place or animal. We really do not know-->
```
# Why XML?

XML would be a great choice to store information about any system, since it has a lot of advantages, for example:

1. Any data can be transferred to XML format.
2. XML files can be sent over the web (HTTP, SOAP)
# XML File Structure

An XML file has 2 main components or parts:

* Prologue
* Body of the document
## Prologue

This line of code contains:

* **The XML declaration**, it tells the interpreter that the file is an XML document.
* Might contain a **DTD declaration link**.
* More processing instructions.

```XML
<?xml version="1.0" encoding="UTF-8 | ISO-8859-1 | windows-1251" standalone="no | yes"?>
```

## Body

In contrast to the prologue, body is a **mandatory** element. It must contain only **one root element** as well as it must be a **well formed document**.

>[!Meaning]- What's well formed document?
>Means that the document has not *syntax errors*.

```XML
<root_element>
	<child_element>
		(...)
		<!--This is a comment-->
	</child_element>
</root_element>
```

### Elements

XML labels have a list of specific features:

* Case sensitive, ``<book>`` is not the same as ``<Book>``
* Normally, each element exists with its _closing tag_ `<book>` `</book>` or if the element do not has any data inside, it can be abbreviated as `<book/>`.
* All the data **must be between elements**.

```XML
<book>
	<title> Database Fundamentals </title>
</book>
```

### Attributes

Every XML element can contain one or more multiple attributes, which are just a key-value pair that go with the declaration of the element, as following:

```XML
<book price="20" coin="Dollar">
	<title>
		Database Fundamentals
	</title>
</book>
```

Constraints:

* Attribute's values must be between `" "`
* An element can contain multiple attributes but each on them has a **unique name**.

### Entity references

One of the disadvantage of using XML files is that we cannot use _reserved symbols_ like `< >` or `&`. To solve this problem, we have something called **entity references**. They are just an alternative way to write special characters on our XML.

To write these symbols with entity references we need to follow this syntax: `&name_entity`. It is used to change the text to an entity reference, as following:

```XML
<example>
	250 &lt; 200
</example>

<!--Interpretation-->
<!--
	<example>
		250 < 200
	</example>
-->
```

| Entity reference | Symbol |
| :--- | ----: |
| `&lt;` | < |
| `&gt;` | > |
| `&amp;` | & |
| `&apos;` | ' |
| `&quot;` | " |
| `&#38;` | Unicode character |

### CDATA Sections

Other way to use special characters is by using the elements called **CDATA Sections**. The XML parser will not take into account the CDATA sections in the interpretation, therefore, all the text inside this block **will appear just as plain text**, as following:

```xml
<example>
	<![CDATA[i < 5 <> &x;]]>
</example>
```
The text displayed will be `i < 5 <> &x;` ... It will not change

## Processing instructions

While [[#Prologue|prologue]] is a special line that must be on top of the XML document, we also have the **processing instructions**.
_Processing instructions_ allow documents to **contain instructions for applications or for the parser**. They are not part of the body, however they can appear anywhere in the document.

```xml
<?xml-stylesheet type="text/xml" href="contactos.xml"?>
```


# XML Namespaces

Element names in XML documents might get into conflict across documents, for example:

```XML
<product>
	<name> Product name </name>
</product>
```

and...

```XML
<customer>
	<name> Customer Name </name>
</customer>
```

To solve this problem we have _**namespaces**_. Namespaces ==turn local names into globally unique names==. It must be specified with the attribute `xmlns` (xml namespace).

```xml
<product xmlns = "https://example.org/product/">
	<name> Product name </name>
</product>
```

## How to use?

* XML namespaces are declared using `xmlns` attribute.
* We can define two types of namespaces
	* `xmln = " "` declares the default namespace
	* `xmlns:prefix = " "` declares namespace _prefixes_.

In order to use prefixes with an specific element of that namespace, we need to type `<prefix:name>`, as following:

```xml
<foo:root
	xmlns:foo="https://example.org/ns2/"
	xmlns:bar="https://example.org/ns3/" 
>
	<bar:element> Test </bar:element>
	<element> This is a name from other namespace </element>
</foo:root>
```

 >[!note] Namespace declaration allows the **mix** of names without conflicts

### More examples...

```XML
<h:html
		xmlns:xdc="http://www.xml.com/books"
		xmlns:h="http://www.w3.org/HTML/1998/html4"
>
	<h:head>
		<h:title> Book review </h:title>
	</h:head>
...
<xdc:bookreview>
	<xdc:title>XML: A Primer</xdc:title>
</xdc:bookreview>
...
</h:html>
		
```

The [[XML DOM|tree diagram]] of the code looks like this:

![[Pasted image 20231022131044.png]]
Notice how we do not conflicts between `h:title` and `xdc:title` elements.