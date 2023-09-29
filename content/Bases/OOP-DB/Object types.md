---
draft: false
title: Object Types
tags:
  - Databases
  - NoSQL
  - Oracle
  - OOP-Databases
---

# Introduction
---
OOP is a useful programming paradigm that helps **reducing code and create reusable components and complex applications**. When we go to No-SQL databases we can find the OOP DB's. This type of databases **implement the same paradigm but adapted to databases**, it is based not in classes but in **object types** (at least in Oracle).
# Object types
---
An **object type** also known as ***UDT (User Defined types)***, is a datatype that ==encapsulates a data structure along with the functions and procedures needed to manipulate the data==. They can be used to represent **entities** such as customers, products, and orders as **a single object that can be shared among applications**.

Imagine you have a jelly mould. This mould will help us creating **tons of jellies**. The same happens when we define an object type, it acts as a mould for further **instances**. 

![[Object-types-illustration.png]]

### Types of UDT's
---
We have two types of UDT's:

> [!caution] This block is incomplete
> This part of the topic is incomplete, I need to describe both of the types of UDT's. However I'm still studying it to make it as easy as possible to explain.

1. Object types
2. Collection types

## How can we create it?
---
Oracle uses a variant of SQL standard called **PL/SQL**, therefore the syntax can change a little bit. We create **simple** object types using the following syntax:

```PLSQL
CREATE OR REPLACE TYPE nameObjectType AS OBJECT (
	attribute_name dataType
);
```

Real code example:

```PLSQL
CREATE OR REPLACE TYPE tipoDireccion AS OBJECT  (
	calle VARCHAR2 (30),
	colonia VARCHAR2 (30),
	ciudad VARCHAR2 (30)
);
/
```

Using APEX service from Oracle Cloud, we can see the created object under the *Types* section of Object Browser

| --- | --- |
| --- | --- |
| ![[Pasted image 20230926114745.png]]    |   ![[Pasted image 20230926115135.png]]  |

## Using the created object
---
Now that we have created or UDT or Object, **how can we use it?**. 
If we were working with tables and we want an attribute of type **tipoDireccion** we might use the following code:

```PLSQL
CREATE TABLE Jugador (
	nombre VARCHAR2 (30),
	vive_en tipoDireccion,
	foto BLOB
);
/
```

![[Pasted image 20230926122319.png]]

Or making a table with the same attributes as the object:

```PLSQL
CREATE OR REPLACE TYPE tipoEmpleado AS OBJECT (
	DNI NUMBER,
	nombre VARCHAR2 (30),
	fecha_nac DATE
);

CREATE TABLE Empleado OF tipoEmpleado;
```

The code will perform 2 tasks:

1. Create an object called *tipoEmpleado* with some attributes
2. Create a table that has the same attributes as the *tipoEmpleado* object, using the clause **OF**

| --- | --- |
| --- | --- |
| ![[Pasted image 20230926122113.png]]    | ![[Pasted image 20230926122135.png]]    |

---
Next topic ➡️ [[Modifying Types]]
