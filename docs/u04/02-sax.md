# 4.2 SAX: analizar sin cargar todo el árbol

En [3.3](../u03/03-programas.md) se leyó la biblioteca con **DOM** (`ElementTree`): el documento entero se carga en un árbol y luego se recorre. **SAX** (*Simple API for XML*) funciona al revés: el analizador recorre el documento **una sola vez, de principio a fin**, y por cada etiqueta que abre, cada etiqueta que cierra y cada trozo de texto llama a un método tuyo. Nunca guarda el árbol: si quieres recordar algo, **tú** decides qué guardar.

## Un manejador (`ContentHandler`)

```python
import xml.sax

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


class ManejadorLibros(xml.sax.ContentHandler):
    def __init__(self):
        self.etiqueta = None
        self.titulo = ""
        self.total = 0.0

    def startElement(self, nombre, attrs):
        self.etiqueta = nombre
        if nombre == "titulo":
            self.titulo = ""

    def characters(self, contenido):
        if self.etiqueta == "titulo":
            self.titulo += contenido
        elif self.etiqueta == "precio":
            self.total += float(contenido)

    def endElement(self, nombre):
        if nombre == "titulo":
            print("Título:", self.titulo)
        self.etiqueta = None


manejador = ManejadorLibros()
xml.sax.parseString(xml_texto.encode("utf-8"), manejador)
print("Total:", round(manejador.total, 2))
```

**Salida:**

```text
Título: Cien años de soledad
Título: El nombre de la rosa
Título: Rayuela
Total: 61.4
```

Fíjate en qué guarda el manejador y qué no: `self.titulo` solo vive mientras se está leyendo **ese** `<titulo>`, y `self.total` es el único dato que sobrevive todo el documento. El título de un libro se imprime en cuanto se cierra su etiqueta (`endElement`), no al final: en SAX los resultados pueden salir **mientras se lee**, antes de terminar el documento.

!!! tip "Cuándo usar cada uno"
    **DOM** (3.3) es más cómodo: navegas el árbol, lo modificas, usas XPath. **SAX** gasta mucha menos memoria porque nunca tiene el documento entero cargado, así que es la opción para documentos **muy grandes** (varios gigabytes) o cuando solo necesitas pasar una vez y quedarte con unos pocos datos, como en este ejemplo.
