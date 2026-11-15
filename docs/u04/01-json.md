# 4.1 XML y JSON

En [1.1](../u01/01-que-es.md#xml-html-y-json) ya se comparó XML con JSON a nivel de concepto. Aquí se convierte **de verdad** la biblioteca de ejemplo en los dos sentidos, con Python y solo la biblioteca estándar (sin instalar nada).

## De XML a JSON

```python
from xml.etree import ElementTree as ET
import json

xml_texto = """<?xml version="1.0" encoding="UTF-8"?>
<!-- Biblioteca de ejemplo -->
<biblioteca>
  <libro isbn="978-84-376-0494-7" genero="novela">
    <titulo>Cien años de soledad</titulo>
    <autor>Gabriel García Márquez</autor>
    <anio>1967</anio>
    <precio moneda="EUR">19.90</precio>
  </libro>
  <libro isbn="978-84-206-3365-1" genero="ensayo">
    <titulo>El nombre de la rosa</titulo>
    <autor>Umberto Eco</autor>
    <anio>1980</anio>
    <precio moneda="EUR">24.50</precio>
  </libro>
  <libro isbn="978-84-663-1840-3" genero="novela">
    <titulo>Rayuela</titulo>
    <autor>Julio Cortázar</autor>
    <anio>1963</anio>
    <precio moneda="EUR">17.00</precio>
  </libro>
</biblioteca>"""

raiz = ET.fromstring(xml_texto)
libros = []
for libro in raiz.findall("libro"):
    libros.append({
        "isbn": libro.get("isbn"),
        "genero": libro.get("genero"),
        "titulo": libro.find("titulo").text,
        "autor": libro.find("autor").text,
        "anio": int(libro.find("anio").text),
        "precio": float(libro.find("precio").text),
    })
print(json.dumps({"libros": libros}, ensure_ascii=False, indent=2))
```

**Salida:**

```text
{
  "libros": [
    {
      "isbn": "978-84-376-0494-7",
      "genero": "novela",
      "titulo": "Cien años de soledad",
      "autor": "Gabriel García Márquez",
      "anio": 1967,
      "precio": 19.9
    },
    {
      "isbn": "978-84-206-3365-1",
      "genero": "ensayo",
      "titulo": "El nombre de la rosa",
      "autor": "Umberto Eco",
      "anio": 1980,
      "precio": 24.5
    },
    {
      "isbn": "978-84-663-1840-3",
      "genero": "novela",
      "titulo": "Rayuela",
      "autor": "Julio Cortázar",
      "anio": 1963,
      "precio": 17.0
    }
  ]
}
```

Dos decisiones que has tomado tú, no el conversor: los **atributos** (`isbn`, `genero`) se han convertido en claves normales, igual que los elementos hijos (`titulo`, `autor`...) — JSON no distingue entre las dos cosas, así que hay que elegir. Y los tres `<libro>` repetidos se han convertido en una **lista** de forma natural, porque JSON sí tiene ese concepto directamente.

## De JSON a XML

Al revés también hay que decidir qué claves se convierten en **atributos** y cuáles en **elementos hijos** (aquí, `isbn` y `genero` como atributos; `titulo` y `autor` como hijos, para que quede parecido a la biblioteca original):

```python
from xml.etree import ElementTree as ET

libros = [
    {"isbn": "000-1", "genero": "poesia", "titulo": "Veinte poemas de amor", "autor": "Pablo Neruda"},
    {"isbn": "000-2", "genero": "teatro", "titulo": "La casa de Bernarda Alba", "autor": "Federico García Lorca"},
]

raiz = ET.Element("biblioteca")
for d in libros:
    libro = ET.SubElement(raiz, "libro", isbn=d["isbn"], genero=d["genero"])
    ET.SubElement(libro, "titulo").text = d["titulo"]
    ET.SubElement(libro, "autor").text = d["autor"]
print(ET.tostring(raiz, encoding="unicode"))
```

**Salida:**

```text
<biblioteca><libro isbn="000-1" genero="poesia"><titulo>Veinte poemas de amor</titulo><autor>Pablo Neruda</autor></libro><libro isbn="000-2" genero="teatro"><titulo>La casa de Bernarda Alba</titulo><autor>Federico García Lorca</autor></libro></biblioteca>
```

!!! tip "Cuándo convertir"
    Si solo necesitas **intercambiar datos** con una API web, trabaja en JSON directamente. Conviertes a partir de XML cuando el documento ya existe en XML (una configuración, un `.docx`, una respuesta SOAP) y el resto de tu programa prefiere trabajar con diccionarios y listas.
