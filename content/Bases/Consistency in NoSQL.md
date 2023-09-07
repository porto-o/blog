---
draft: false
tags:
  - Databases
title: Consistency in NoSQL
---
# Introduction

Si haz trabajo con sistemas de bases de datos relacionales, lo más seguro es que conozcas el término **"consistencia de datos"**. Este término hace referencia a que todos los datos cumplen con un esquema o formato específico, siguiendo restricciones y eliminando las redundacias que se puedan originar.

# Qué pasa en los sistemas NoSQL?

## Estrategias de escalamiento en NoSQL

Antes de abordar el tema de consistencia de datos en sistemas no relacionales, voy a hablar un poco sobre las 2 formas que tenemos para escalar nuestro sistema NoSQL

* **Escalamiento vertical**:  Este tipo de escalamiento es muy sencillo de entender, ya que simplemente hace referencia al incremento de capacidad de cómputo de nuestra máquina, es decir, a cambiar nuestro hardware por alguno más potente.

* **Escalamiento horizontal**: Por otro lado, el escalamiento horizontal hace referencia a una malla de computadoras con capacidades de cómputo similares. Estas computadoras se **reparten** los datos de tal forma que el procesamiento sea similar en cada uno de los nodos.

## Sharding

Cuando elegimos un escalamiento horizontal, normalmente nos referimos a una técnica llamada *Sharding*.

### Qué es sharding?

Sharding se refierre a una técnica de particionamiento de datos, de tal forma que aquellos datos que son consultados con más frecuencia, estén siempre disponibles en el mismo nodo.

> [!note]
> Para hacer un buen Sharding, se debe tener en cuenta que la carga de datos debe quedar distribuida entre todos los nodos del sistema de la manera más homogénea posible.

Estos fragmentos, nodos o *shards*, tienen su propio **conjunto de replica**. Este conjunto son como respaldos de la data que se encuentra en el nodo principal, de tal forma que si falla el componente principal, sus **réplicas** podrán solventar el problema.

![[Pasted image 20230907010356.png]]

### Consideraciones

En este tipo de escenarios, el fenómeno de **inconsistencia** de datos se genera de manera natural. Ya que el tiempo en que las copias logran obtener un nuevo dato o datos actualizados, perjudica mucho en esta consistencia. Sin embargo, a este tipo de inconsistencia se le llama **consistena eventual**, es decir, en algún momento el sistema podrá volver a ser consistente (microsegundos, segundos, minutos, etc).

---
Next topic ➡️ [[CAP theorem]]