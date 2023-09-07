---
draft: false
title: Key-value databases
tags:
  - Databases
  - NoSQL
---
# Introduction

Key-value database is by far the most popular type of NoSQL system. It works in a pretty simple way:

> Each element or value, is identified by a **unique key** which is not necessarily an integer. 

This feature allows a **high-speed data read** process since knowing the key will return the data immediately. Furthermore, the data stored is usually **binary objects** or **BLOB** (multimedia).

# Limitations

It has not a defined schema since all the stored items are just binaries. For instance, a record of a person could have **name, address and phone number**, while other record might contain only **name and email**.

In addition, key-value stores **have not** query language and because of this, values cannot be queried or searched upon, **only the key can be queried**.

![[Pasted image 20230907102229.png]]

# How it works?

This type of NoSQL database uses a hash function to store unique keys **along with the pointers to the corresponding data values**. These values can be of simple format such as scalar or complex formats such as JSON or BLOB.

![[Pasted image 20230907110315.png]]

# Examples

1. Cassandra
2. BigTable
3. Hbase