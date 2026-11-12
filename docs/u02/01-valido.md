# 2.1 Bien formado y válido

Hay **dos niveles** de corrección en un documento XML:

| Nivel | Qué comprueba | Quién lo exige |
|---|---|---|
| **Bien formado** | Que respeta las **reglas de escritura** de XML (etiquetas cerradas, anidadas, comillas…) | Todos los analizadores, siempre |
| **Válido** | Que además cumple una **estructura concreta** definida en un esquema (qué elementos, en qué orden, de qué tipo) | Solo si se pide validar |

Un símil: una frase **bien formada** es la que está bien escrita (sujeto, verbo, puntuación); una frase **válida** es la que además cumple las reglas de un formulario concreto («escriba su DNI: 8 números y una letra»).

Este documento está bien formado:

```xml
<biblioteca><libro><titulo>Rayuela</titulo></libro></biblioteca>
```

pero **no es válido** si la biblioteca exige que cada libro tenga autor, año y precio. Un validador lo dice así:

**Mensaje del validador (DTD):**

```text
Element libro content does not follow the DTD, expecting (titulo , autor+ , anio , precio), got (titulo)
```

## Para qué sirve validar

* **Detectar errores** de datos antes de procesarlos (un precio que no es un número, un campo que falta).
* Ser un **contrato**: quien genera el XML y quien lo lee se ponen de acuerdo en la estructura.
* Que el editor **ayude**: con un esquema, un buen editor autocompleta etiquetas y avisa de errores mientras escribes.

## Cómo se describe una estructura

Dos lenguajes estándar, que veremos a continuación:

* **DTD** (*Document Type Definition*): el más antiguo, con su propia sintaxis, sencillo pero limitado ([2.2](02-dtd.md)).
* **XML Schema (XSD)**: más potente, escrito **en XML** y con tipos de datos ([2.3](03-xsd.md)).

Los dos describen lo mismo que se ve en la biblioteca de ejemplo: un `libro` tiene un `titulo`, uno o más `autor`, un `anio` y un `precio`.
