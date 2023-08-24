---
title: Databases
draft: false
tags:
  - DP-900
  - Databases
  - SQL
---
## What is a database?

A database is a **file system** on which files are stored or a **dedicated system for managing data records**.

There are several types of databases, for instance:

* [[#Relational databases]]
* [[#Non-relational databases]]
---
## Relational databases

This type of database is commonly used to stored [[Data formats#Structured Data|structured data]], since they have a specified schema from the beginning.
The way data is stored is by using **tables which represent _entities_**

>[!note] What is an entity?
>An entity is an abstraction of a real-world object. For example, the entity student, the entity school, the entity teacher and so on.
>Each table represents a real-world object along with its attributes.

Let's imagine we have a database that stores the data from a deli. Probably we'll have the following entities:

* Costumer
* Product
* Order
* Line Item

Each record stored in the database will be called **instance of an entity**, and we can identify every record using **primary keys**. 
Not only does primary keys serves as unique identifiers, but also to reference the instance in other tables.

>[!example] Example
> Customer primary key could be referenced in Order entity to identify the order of a specific client.

This use of keys to reference data enables a relational database to be **normalized**.

>[!note] What is normalization?
>Normalization on databases is the process where we delete duplicated data so that it is stored only once in our database.

![[Pasted image 20230823233823.png]]

---

## Non-relational databases

These databases are the ones that don't apply a relational schema to store the data, i.e it is not necessary to keep a relation between entities.

In contrast of relational databases, there are several types of non-relational databases, the most common are:

### Key-value databases

Each record consist of a unique identifier and the associated value.

![[Pasted image 20230823234321.png]]

### Document databases

This type of non-relational db is actually an specific case of key-value database. However, in document databases the values are stored as JSON objects.

![[Pasted image 20230823234427.png]]

### Column family databases

This type of database group or comprise rows and columns into column-families. Each column family holds a set of columns that are logically related together.

![[Pasted image 20230823234555.png]]

### Graph databases

Entities are stored as nodes and they keep a relation as a graph.

![[Pasted image 20230823234641.png]]

---

|      |     |
|  -- | --- |
| Next topic | ➡️ [[OLTP]] |
| Previous topic | ⬅️ [[File storage]] | 