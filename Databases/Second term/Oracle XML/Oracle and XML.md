Let's take a look at the XML support implementation that Oracle has added to its database. Oracle's implemented tons of tools to store and manipulate XML documents in its database, for example:

* It allows us to **store documents as _columns_**.
* External access to XML documents.
* Map XML documents to tables and columns.
* In Oracle 9i, ==XMLType is introduced to native manage of XML documents==.

# Oracle XML-DB

>[!Warning] TODO
> - [ ] Timeline of Oracle XML-DB

# Storage

Oracle uses two ways to store XML documents
## Data repository (Oracle XML DB Repository)

Hierarchy organized i.e. XML are stored and can be visualized as a tree of directories. Therefore, to access these XML content we must follow one of the following techniques:
* XPath
* URLs --> HTTP / FTP
* SQL and PL/SQL
## Native data type (XMLType)

Oracle includes a native data type for XML documents. This type allows us to define tables, columns, parameters, return values or procedure values as XMLType.

Furthermore, it includes a set of **predefined functions** to create instances, validate content (XML and XMLSchema), apply style sheets, etc.

![[Pasted image 20231022012704.png]]
