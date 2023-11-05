# Basic workflow example

Now let's go deep to how to store XML documents in Oracle.

## Create table

For this example I will show you how to add a column of `XMLType` called `resume`. This column **will store the resume of the current person**.

Let's create a table called `employees`.

```SQL
CREATE TABLE employees (
	id CHAR (6),
	name VARCHAR (30),
	resume XMLType
);
```
 After executing the previous code in APEX, we will have something like...
 
![[Pasted image 20231022135207.png]]

## Add data

Now, let's add some data to our table. For the resume column we will insert **an entire XML document**, therefore, will the insert operation be the same as for other attributes?

For short, no. We will need to "call the constructor" of XMLType and pass the entire document, as following:

```SQL
INSERT INTO employees (id, name, resume) VALUES (
	1,
	'Ismael Porto',
	XMLType('<?xml version="1.0" encoding="UTF-8"?>
<resume>
    <personal_information>
        <name>John Doe</name>
        <contact_information>
            <email>john.doe@email.com</email>
	           ...')
);
```

The xml is too long, therefore I did not write the whole code.

After executing the insert operation, we will have something like...

![[Pasted image 20231022135802.png]]

Alright, we've added our first record to the table employees with a column of XMLType. However, as you've noticed, in the resume column we only have `[XMLTYPE]` object. **How can we get the actual value of that object**?

## Retrieve data

To get the actual value of an XMLType record what we need to do is **use the functions of Oracle-XML**, in this example I will use `extract()` function, however you must know that there are a lot of functions to manipulate XML documents, which I will address later.

```SQL
SELECT extract(resume, "/resume") FROM employees;
```

Do not worries If you don't understand the syntax, I will explain this and other function later on the topic.

What we are doing is retrieving all the document after `/resume` element of the document. The output of the code will look like this.

![[Pasted image 20231022140458.png]]

# Oracle and XML

In Oracle we have two way to store XML data

1. XMLType columns
2. XML Object based tables: `CREATE TABLE MyTable OF XMLTYPE;`

---
Next ➡️ [[XML Schema validation in Oracle database]]
