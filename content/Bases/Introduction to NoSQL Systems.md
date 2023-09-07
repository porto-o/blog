---
draft: false
title: Introduction to NoSQL Systems
tags:
  - Databases
---
---
# Qué son los sistemas NoSQL?

En términos simples, un sistema NoSQL es aquel que difiere de un sistema relacional de base de datos en varios aspectos, el más destacado es que **no usan SQL para hacer consultas a las bases de datos**.

# Cómo surgen?

Con la llegada de la Web 2.0 en los años 2000 se generó un incremento  en las necesidades de almacenamiento de datos, debido a que nuevas plataformas como Facebook, Twitter o Youtube, permitían que sus usuarios subieran multimedia. Esto derivó en un problema de rendimiento, el cuál tarde o temprano lo tenían que optimizar.

# Cómo se encuentran los datos?

Los datos almacenados no necesariamente cumplen con un formato tabular, sino que estos se pueden presentar en [[Databases#Non-relational databases|diferentes formatos]]. Entre las características principales de estos sistemas de bases de datos se encuentran:

1. No garantizan cumplir con las propiedades ACID de un sistema relacional
2. No soportan operaciones JOIN
3. Suelen tener un mejor escalamiento horizontal, que vertical.

Finalmente, cabe destacar que este tipo de bases de datos están optimizadas para las operaciones de **lectura y agregamiento**.

# Diferencias con un esquema relacional

| NoSQL | Relacional |
| --- | --- |
| No utilizan SQL como lenguaje de consultas | Utilizan SQL para consultas |
| Utilizan diferentes estructuras para almacenar los datos, por ejemplo, clave-valor | Utilizan el formato tabular para el almacenamiento de los datos |
| No permiten operaciones JOIN | Permiten operaciones JOIN |
| Suelen estar en una **arquitectura distribuida**, es decir, la información puede estar compartida en varias máquinas. | Normalmente se encuentran centralizadas | 

---
Next topic ➡️ [[Consistency in NoSQL]]