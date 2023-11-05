# First steps

If you remember XML Schema helps us validate our XML document, therefore there must be a way to validate it but in a database. Oracle Database allows us to have an XML Schema, however we must perform some previous task.

* Create a directory in our OS where we will be saving XML and XML Schema documents.
* Connect the server with this directory using DBA user i.e. **create a `DIRECTORY` Oracle object and connect that object to the actual directory where my file are stored**, as following:

```SQL
CREATE DIRECTORY DIRECTORY_NAME AS '/path_XML';
GRANT READ, WRITE ON DIRECTORY_NAME "DOCUMENTS_XML" TO user;
```
# Register the Schema

After connecting Oracle Database Server to our directory, what we need to do is to register our schema:

```SQL
BEGIN
	DBMS_XMLSCHEMA.REGISTERSCHEMA(SCHEMAURL => 'URL', SCHEMADOC => BFILENAME('DIRECTORY_NAME','file.xsd'), GENTYPES=>FALSE, GENTABLES=>FALSE);
END;
/
```

URL parameter is like an identifier and `file.xsd` is the XML Schema document. In order to check if our schema has correctly registered, we can execute:

```SQL
SELECT SCHEMA_URL, LOCAL, XMLSERIALIZE(DOCUMENT SCHEMA AS VARCHAR(4000)) FROM USER_XML_SCHEMAS;
```

# Use the Schema

After registering the Schemas, we can use them to create XMLType tables and perform validations according with the XML Schema. For example, let's create again the table `employees`.

```SQL
CREATE TABLE employees OF XMLType XMLSCHEMA "URL" ELEMENT "rootName_xml";
```

`URL`: Refers to the previous url generated when registering the schema.
`rootName_xml`: Refers to the root name of the XML document to validate.

Other approach is by using the XMLType but in columns, therefore the code should look as following:

```SQL
CREATE TABLE employees (
	id NUMBER, 
	document XMLType
) XMLTYPE COLUMN document XMLSCHEMA "URL" ELEMENT "rootName_xml";
```

## Verify the table

In order to verify if our XMLType table has been correctly created, we can query the data dictionary of Oracle DB.

```SQL
SELECT TABLE_NAME FROM USER_XML_TABLES;
```

Furthermore, we have access to a set of _informative schema functions_ 

* `isSchemaBased()`
* `isSchemaValid()`
* `isSchemaValidated()`

Each one returns 1 if true or 0 in any other case.

* `getSchemaURL()`: Returns the url of the associated schema.
* `schemaValidate()`: Performs a validation on an XML document.

# Insert values

To insert XML documents in a XML table we have two choices

* Insert directly the XML on the `INSERT` statement
* Specify the path of the document to be inserted.

```SQL
INSERT INTO xml_table VALUES(
	XMLType(BFILENAME('Directory', 'document_name.xml'), nls_charset_id('AL32UTF8'))
);
```

# Validation functions

We can perform XML Schema validation before and after an insertion on the database. For example, let's see how to **perform a validation before insertions**.

```SQL
CREATE OR REPLACE TRIGGER validate_employee
	BEFORE INSERT ON employees FOR EACH ROW
BEGIN
	IF (:new.OBJECT_VALUE IS NOT NULL) THEN :new.OBJECT_VALUE.schemavalidate(); END IF;
END;
```

This is **different from the schema association when creating the table**. When we created the table we specified that it must contain an XML Schema validation. However, this validation will not take effect before insertions, **only after insertions**.

Apart from the trigger approach, we can also specify a constraint with `CHECK` clause

```SQL
ALTER TABLE table_name ADD CONTRAINT chk_validate_table CHECK (XMLIsValid(OBJECT_VALUE) = 1);
```

On the other hand, I we wanted to validate data after insertions, we can do it with the following code:

```SQL
SELECT t.xmlcol.isSchemaValid('xsd_path', 'Tables') FROM tables t;
```

