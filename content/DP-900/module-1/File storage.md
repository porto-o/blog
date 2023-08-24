---
title: File storage
draft: false
tags:
  - DP-900
---

## Introduction

There are tons of data formats, from _docx_ documents through _.py_ files. However, we must know that the data format will depend on the following factors:

1. If it is structured, semi-structured or unstructured data
2. The applications of that content, for instance, read, write, etc.
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

![[Pasted image 20230823193546.png]]

However, if you remember [[Data formats#Unstructured data|unstructured data]] concept, you know that the data is stored as **row binary**, which means that these files **have not format in any way**, for example, images or videos. Since these files have not format at all, the amount of binary numbers is enormous. To solve this, applications interpret these raw binary formats and **render it**.

This is why we called BLOBs (Binary Large Objects), since they have tons of unstructured binary data.


---

## Optimized file formats

Nowadays, with the increment of big data, organizations must store their data in a way that allow them to **optimize storage, processing, etc**. In light of this, some specialized file formats have been created, the most know are:

1. [[#Avro]]
2. [[#ORC (Optimized Row Columnar format)]]
3. [[#Parquet]]
### Avro

It is a **row based** format created by Apache. Each record contains a **_header_ in JSON format**, that **describes the structure of the data** in the record.

The **actual data is stored as binary information**, so in order to extract the fields each record contains, an applications uses the **information form the header to parse the binary data**.

== Avro **minimizes storage and network bandwidth requirements** ==

![[Pasted image 20230823193622.png]]

---
### ORC (Optimized Row Columnar format)

This type of format **organizes data in columns rather than rows**. It was developed by HortonWorks for **optimizing read and write operations** in [Apache Hive](https://hive.apache.org/).

This format provides **quick and efficient access to data**.

![[columndar_data.png]]

#### How is the data organized in ORC files?

First and foremost, ORC files are mainly **divided into _stripes_**.

>[!note]
>Stripes are just segmentations of our data

Each stripe is divided in **three parts**.


|       |  | |
| ----------- | ----------- | ----- |
| Index      |    ![[index_data.png]]    | It includes **min and max** values for each column and a **range of positions within each column**|
| Row data   |     ![[raw.png]]    | It includes the unprocessed data, organizing each attribute on **independent columns**| 
| Footer |     ![[footer.png]]       | Contains a **directory** of stream locations |

>[!info]
>The following image illustrates two stripes.
>* The index block is pointing to the stack of columns with the min and max values
>* The row data block is pointing to the actual data
>
>![[Pasted image 20230823183908.png]]


>[!example] Index Block Example
>
> Let's imagine an ORC file that stores online sales data from a virtual store. Each sale is recorded with attributes such as _sale ID, product name, price, quantity sold, purchase data_.
> 
> The example focuses on a specific sales day's "stripe" within the ORC file. Let's suppose this stripe contains sales data from January 1 2023. Within the stripe you'll find the data of sales made on that day, as following:
> 
> _Stripe index (Example for a sales day)_
> * Column: Sale ID
> 	* Minimum and maximum values: [1001, 1500]
> 	* Location in the stripe: 5000 - 8000
> * Column: Price
> 	* Min and max values: [10.99, 49.99]
> 	* Location in the stripe: 10000 - 13000

---
### Parquet

Parquet is a **columnar data format** too. It was developed by Cloudera and Twitter (X now). To begin with the explanation, let's illustrate the difference between row and columnar data inside the hard drive:

Let's imagine we have the following data

![[Pasted image 20230823190733.png]]

#### Row-oriented data on disk

If we used row oriented files, the data inside the disk would look like this:

![[Pasted image 20230823190825.png]]

Each record is saved along with its attributes.

#### Column-oriented data on disk

On the other hand, If we used column oriented files, the data inside the disk would look like this:

![[Pasted image 20230823190938.png]]

If you notice, data is **organized in groups**. For instance, the first 3 blocks might be from the _title column_.

---

Now that you've understood the difference on hard drive, let's explain Parquet files.
Parquet files are a combination of both row and columnar formats. Inside the disk, the parquet files store their data as following:

![[Pasted image 20230823192052.png]]

Parquet organizes the data in **row groups** and each **row group contains one or more chunks of data**.

>[!Example]Parquet data blocks
>![[Pasted image 20230823192313.png]]

---
#### Under the hood

Every Parquet file is composed by:
* A header
* Data blocks
* A footer
Using these components, parquet files store **two** types of data:
1. Metadata --> Header and footer
2. Data --> Data blocks

>[!Example]Parquet file overview
>![[Pasted image 20230823192600.png]]


An application can use _metadata_ to **quickly locate the correct chunk for a given set of rows**.

#### Summing up Parquet files

Parquet files were created to improve queries since it specializes in storing and processing nested data type **efficiently**.

## Conclusion

Now that you've learned the most common data formats in both common scenarios and specialized scenarios, you should be able to work with different formats as well as decide which format is the best for your purposes.

You can learn more about specialized file formats in the following links:

* [IBM Avro]( https://www.ibm.com/topics/avro#:~:text=Avro%20files%20include%20markers%20that,it%20ideal%20for%20scripting%20languages.)
* [ORC Files](https://www.upsolver.com/blog/the-file-format-fundamentals-of-big-data#:~:text=The%20ORC%20file%20format%20stores,reduce%20read%20and%20decompression%20loads.)
* [Databrick Parquet docs](https://www.databricks.com/glossary/what-is-parquet#:~:text=What%20is%20Parquet%3F,handle%20complex%20data%20in%20bulk.)
---
|      |     |
|  -- | --- |
| Next topic | ➡️ [[Databases]] |
| Previous topic | ⬅️ [[Data formats]] | 
