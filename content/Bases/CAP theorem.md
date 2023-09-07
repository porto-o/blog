---
draft: false
title: CAP Theorem
tags:
  - Databases
---
# **Introduction**

El teorema CAP nos dice que **en sistemas distribuidos es imposible garantizar que la consistencia, la disponibilidad y la tolerancia a particiones, se encontraran juntos**. Es decir, un sistema no puede contar con estos 3 atributos al mismo tiempo.

# Terms meanings

1. Consistencia: Se refiere a que todos los usuarios pueden ver **los mismos datos en cierto instance**.

2. Disponibiilidad: La base de datos **no deja de funcionar ante fallas**

3. Tolerancia a particiones: El sistema no deja de funcionar ante **fallas en la red de comunicación entre nodos**.

# So then... how can they be scalable and distributed?

NoSQL systems use different methods to achieve a great level of scalability and perfect for distribution.

* AP
* CA
* CP

![[Pasted image 20230907012151.png]]

However, because of the CAP theorem, there is not a service that could achieve the 3 key features.

---
Next topic ➡️ [[NoSQL Databases classification]]