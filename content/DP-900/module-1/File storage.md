---
title: File storage
draft: false
tags:
  - dp900
  - module-1
---

## Introduction

There are tons of data formats, from _docx_ documents through _.py_ files. However, we must know that the data format will depend on the following factors:

1. If it is structured, semi-structured or unstructured data
2. The applications of that content, for instnace, read, write, etc.
3. The need of readability, if it is for human reading or not.

## Common files formats

### Delimited text files

The data is organized in rows, where each field is separated by a symbol. For instance, commas, periods, slashes, etc.

One of the most famous data format with these features is the _csv_.

> [!example]
>
> ```csv
> FirstName, LastName, Email
> Joe, Jones, joe@litware.com
> Samir, Nadoy, samir@northwind.com
> ```

### JavaScript Object Notation (JSON)

Ubiquitous format in which **each object is an _entity_, that can have multiple attributes**.

> [!example]
>
> ```json
> {
>   "customers": [
>     {
>       "firstName": "Joe",
>       "lastName": "Jones",
>       "contact": [
>         {
>           "type": "home",
>           "number": "555 123-1234"
>         },
>         {
>           "type": "email",
>           "address": "joe@litware.com"
>         }
>       ]
>     },
>     {
>       "fistName": "Samir",
>       "lastName": "Nadoy",
>       "contact": [
>         {
>           "type": "email",
>           "address": "samir@northwind.com"
>         }
>       ]
>     }
>   ]
> }
> ```

### Extensible Markup Language (XML)

This is a most comfortable data format to work with, since it has a **human-readable** focus. It is superseded by the less verbose JSON and it uses **tags to define elements and attributes**.

> [!Example]
>
> ```xml
> <Customers>
>  <Customer name="Joe" lastName="Jones">
>    <ContactDetails>
>      <Contact type="home" number="555 123-1234" />
>      <Contact type="email" address="joe@litware.com" />
>    </ContactDetails>
>  </Customer>
>  <Customer name="Samir" lastName="Nadoy">
>    <ContactDetails>
>      <Contact type="email" address="samir@northwind.com" />
>    </ContactDetails>
>  </Customer>
> </Customers>
> ```

### Binary Large Object (BLOB)

Although all fancy syntax, everything is stored as 0's and 1's. So then, how can we understand some files if everything is stored as binary numbers?

Programs such as word or excel, **map binary data to printable characters**. For instance, if in my file there is a line with the number 01001010. The steps for mapping this to a human-readable character are the following:

* 01001010 is converted into decimal
* 01001010 in decimal is 74
* Typically we use ASCII table to map numbers to letters. In this case 74 is J
* So now, the data displayed is J

_INSER PICTURE OF ASCII TABLE_

However, if you remember [[Data formats#Unstructured data|unstructured data]] concept, you know that the data is stored as **row binary**, which means that these files **have not format in any way**, for example, images or videos. Since these files have not format at all, the amount of binary numbers is enormous. To solve this, applications interpret these raw binary formats and **render it**.

This is why we called BLOBs (Binary Large Objects), since they have tons of unstructured binary data.


---

## Optimized file formats

Nowadays, with the increment of big data, organizations must store their data in a way that allow them to **optimize storage, processing, etc**. In light of this, some specialized file formats have been created, the most know are:

1. [[# Avro]]
2. [[# ORC (Optimized Row Columnar format)|ORC]]
3. Parquet
### Avro

It is a **row based** format created by Apache. Each record contains a **_header_ in JSON format**, that **describes the structure of the data** in the record.

The **actual data is stored as binary information**, so in order to extract the fields each record contains, an applications uses the **information form the header to parse the binary data**.

== Avro **minimizes storage and network bandwidth requirements** ==

_INSERT IMAGE_

### ORC (Optimized Row Columnar format)