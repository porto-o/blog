---
draft: false
title: Modifying UDT's
tags:
  - Databases
  - NoSQL
  - Oracle
  - OOP-Databases
---
# Introduction
---
Up to this point we have created our own object types and learned how to use them. However, what if in the future we want to modify their structure, how can we do it?

# Add attributes to object types
---
For example, what if to the object type called *tipoEmpleado* I wanted to add an attribute called *gender*.

==The syntax to modify the **structure** of an object type already declared is the following==

```PLSQL
ALTER TYPE typeName ADD ATTRIBUTE attribute_name data_type CASCADE;
```

>[!Question]- Why **CASCADE**?
>
>The cascade clause allows us to let Oracle know that the task must be performed through all the object type instances. For instance, in the previous examples we have created a table called *Empleado* which had the same attributes as the *tipoEmpleado* object, If we just put the statement without the **cascade** clause, it will cause an error because we already had instances of that object. To sum up, cascade performs a 'cascade behavior's' altering an object throughout all its instances.

After altering the *tipoEmpleado* object type, we must have the following table. Notice how the table also has been updated. *I just add the attribute **gender***.

![[Pasted image 20230926130118.png]].

# Instantiable objects
---
To begin with, let's explain what is an **instantiable object**.

When we create an object type, what we really create is a mould. This mould will be the base of further objects, for example the jelly mould can be useful for different jellies. An object is instantiable when we **can create instances from that object type**.

In the following example we can create two instances from the object *tipoEmpleado*:
1. tipoOperativo
2. tipoDirectivo

![[Pasted image 20230928192351.png]]

## How can it be specified?
---
To specify that an object will be **instantiable** we must type the following code:

```PLSQL
ALTER TYPE nameObject [NOT] INSTANTIABLE
```

If we type decide to make an object *not instantiable* then we will be getting something called **abstract objects**, which in OOP is known as **abstract classes**. 

# FINAL and NOT FINAL objects
---
When we specify that an object must be **FINAL**, what we're really saying to SQL is that **the object cannot have inheritance**. The code of this will look as following:

```plsql
ALTER TYPE nameObject [NOT] FINAL;
```

>[!Warning]- WHAT YOU MUST KNOW
>Every object that we create in Oracle will have the FINAL clause as default, thus, we won't be able to make inherited objects.

In the following image we can see that **tipoEmpleado** object might be *NOT FINAL* whereas **tipoEstudiante** might be *FINAL*. Furthermore, **tipoPersona** must be **INSTANTIABLE**.

![[Pasted image 20230928192351.png]]

# Add methods to objects (classes in OOP)
---
If you ever worked with low-level programming languages like C, you should be familiar with the concept of **prototype**, which is just a way to **tell the compiler the name of the function, the data types of the parameters and the return**. Furthermore, this will help us to declare functions below the main function.

The same happens on PL/SQL, to create **methods of object types** we must follow 2 steps:

1. Declare the prototype of the *function* or *procedure*.
2. Declare the **body** 

>[!Note]- Consideration
>Please take in mind that I will explain the *member methods*, this methods are **associated with the instance not with the object**. They **operate with the attributes of that object**.

To specify the declaration of the method we will follow this syntax:

```PLSQL
ALTER TYPE objectType ADD MEMBER { FUNCTION | PROCEDURE } methodName RETURN typeReturn CASCADE;
```

>[!Note]
>We can also specify the methods when we create the object, however to make it as simple as possible I've explained as an *alter type* operation.

After the declaration we must create the body of that method, we will achieve this following this syntax:

```PLSQL
CREATE OR REPLACE TYPE BODY objectType AS .............
```