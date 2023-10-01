---
draft: false
title: Inheritance
tags:
  - Databases
  - NoSQL
  - Oracle
  - OOP-Databases
---
# Introduction
---
When we use the OOP in programming, we usually use something called *inheritance*. This concept describes the **behavior's class**, **it allows the definition of *subclasses* under a *superclass***. This subclass inherits attributes and methods of the superclass, however it can also has their owns.

# Inheritance in Databases
---
When we talk about inheritance in the context of OODB's what we refer is to the **ability to define objects that inherit attributes and methods from super-objects**. For example, in the following image we see 5 different objects, each one with their **own attributes along with the parent object's attributes**.

![[Pasted image 20231001153913.png]]

What we really see is a *hierarchy* of objects. The object called *tipoPersona* is the parent of all the other objects. To achieve this behavior we need to define an **[[Modifying Types#Instantiable objects|instantiable object]]**. 

Furthermore, if you see we have **tipoPersona** object you will notice that it does not have children objects. This is because this object contains the clause **FINAL**.

==The clause FINAL or NOT FINAL will tell sql that this object cannot serve as parent object to inheritance.==

>[!Note]
>The clause FINAL is not mandatory since SQL will put it as default, however to specify that an object can have objects UNDER it, wee need to specify it as NOT FINAL

# Example
---

Let's create the code for the previous tree of objects:

## Creating tipoPersona type
---
```PLSQL
CREATE TYPE tipoPersona AS OBJECT (
	DNI VARCHAR(9),
	nombre VARCHAR(25),
	fecha_nac DATE,
	direccion VARCHAR(100)
) NOT FINAL;
```

### Output (Using Oracle - APEX)
---
![[Pasted image 20231001155828.png]]

## Creating tipoEmpleado
---
This types inherit from *tipoPersona*, to make SQL noticed we need to use *UNDER* clause..

```plsql
CREATE TYPE tipoEmpleado UNDER tipoPersona (
	NoTrabajador NUMBER,
	salario NUMBER
) NOT FINAL;
```

### Output
---
Notice how **tipoEmpleado** has 6 attributes, 4 from the parent object and 2 personal.

![[Pasted image 20231001160030.png]]

## Creating tipoEstudiante
---
```PLSQL
CREATE TYPE tipoEstudiante UNDER tipoPersona (
	noBoleta NUMBER,
	carrera VARCHAR(100)
);
```

### Output
---
![[Pasted image 20231001160502.png]]
## Creating tipoOperativo
---
```PLSQL
CREATE TYPE tipoOperativo UNDER tipoEmpleado (
	area VARCHAR(20)
);
```

### Output
---
![[Pasted image 20231001160517.png]]

## Creating tipoDirectivo
---
```PLSQL
CREATE TYPE tipoDirectivo UNDER tipoEmpleado (
	puesto VARCHAR(25),
	oficina VARCHAR(10)
);
```

### Output
---
![[Pasted image 20231001160526.png]]

Up to this point we already have the structure of our hierarchy, however let's add some random data to see how it is in functionality.

## Add data
---
To add the data we will use *tables*. So, the first step is to create a table from the parent object

```PLSQL
CREATE TABLE persona OF tipoPersona;
```

### Output
---
![[Pasted image 20231001161428.png]]

Inserting the data

```PLSQL
INSERT INTO persona VALUES (
	'12345',
	'Juan Perez',
	TO_DATE('12/4/1978', 'dd/mm/yyyy'),
	'Av. Palmas 23, Villas, Toluca'
);
```

![[Pasted image 20231001161627.png]]

## Inserting data into children objects
---
We just put in some data into the parent object, however if we need to add data based on children objects, will it be the same syntax?

The answers is ==depending on how many additional attributes you have==. To explain this let's create the table of tipoEmpleado

```PLSQL
CREATE TABLE empleado OF tipoEmpleado;
```

![[Pasted image 20231001165342.png]]

Now let's add the data

```PLSQL
INSERT INTO empleado VALUES (
	9876,
	8756.50
)
-- Will this code work?
```

The output of this code will be an error. The error says that **we are missing or passing more arguments than the necessary**. However, if we remember, *tipoEmpleado* only has 2 attributes, so... **what is the problem?**

![[Pasted image 20231001165552.png]]

The problem is that we are using inheritance, therefore the attributes of the parent will pass through all the children, along with the personal attributes of each children. *To solve* this problem we need to specify every argument from the parent and the arguments from the children, as following:

```PLSQL
INSERT INTO empleado VALUES (
    '45678',
    'Laura Lopez',
    TO_DATE('9/11/1996', 'dd/mm/yyyy'),
    'Cadiz 564',
	9876,
	8756.50
)
```

![[Pasted image 20231001170320.png]]

Let's add the data for the missing objects

```PLSQL
CREATE TABLE operativo OF tipoOperativo;

INSERT INTO operativo VALUES (
	'86420',
	'Jose Aguado',
	TO_DATE('23/9/1982', 'dd/mm/yyyy'),
	'Calle 34 #298, Oriente, Ecatepec',
	6754,
	6789.00,
	'Soporte'
);

CREATE TABLE directivo OF tipoDirectivo;

INSERT INTO directivo VALUES (
	'97642',
	'Ana Padilla',
	TO_DATE('7/3/1992','dd/mm/yyyy'),
	'Juan Escutia 213, Alamedas, Izcalli',
	8798,
	9782.80,
	'Director de Personal',
	'C-14'
);
```

---
Next topic ➡️ [[Abstract types]]