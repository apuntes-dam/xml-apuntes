# 1.1 Qué es XML

**XML** (*eXtensible Markup Language*, lenguaje de marcas extensible) es una forma de escribir datos y documentos como **texto** con una estructura de **etiquetas** anidadas. Lo define el W3C, es independiente del sistema operativo y del lenguaje de programación, y lo lee tanto una persona como un programa.

```xml
<alumno>
  <nombre>Ana</nombre>
  <nota>8.5</nota>
</alumno>
```

## Un metalenguaje

XML **no tiene etiquetas propias**: no existe `<alumno>` ni `<nota>` «en XML». Es un **metalenguaje**: un lenguaje para **crear otros lenguajes**. Tú (o un estándar) decides qué etiquetas hay y qué significan, y XML solo fija las **reglas de escritura**: cómo se abre y se cierra una etiqueta, cómo se anidan, cómo se ponen atributos.

!!! info "Frente a HTML"
    HTML tiene un conjunto **cerrado** de etiquetas (`<p>`, `<a>`, `<table>`) pensadas para **mostrar** una página. XML tiene un conjunto **abierto** pensado para **describir datos** y su estructura, no su aspecto.

## Lenguajes que se escriben con XML

Muchos formatos conocidos son «XML con un vocabulario concreto»:

| Lenguaje | Para qué sirve | Ejemplo |
|---|---|---|
| **XHTML** | HTML escrito con las reglas estrictas de XML | `<p>Hola</p>` |
| **SVG** | Gráficos vectoriales (logos, iconos) | `<circle cx="50" cy="50" r="40"/>` |
| **MathML** | Fórmulas matemáticas | `<mi>x</mi><mo>+</mo><mn>1</mn>` |
| **GML** | Datos geográficos (puntos, líneas, polígonos) | `<gml:Point>…</gml:Point>` |
| **RSS / Atom** | Noticias y canales que se siguen con un lector | `<item><title>…</title></item>` |
| **XSLT** | Transformar un XML en otro documento | `<xsl:template match="/">` |
| **XSD** | Describir la estructura que debe tener un XML | `<xs:element name="libro"/>` |

Y muchos formatos del día a día: el `AndroidManifest.xml` y los *layouts* clásicos de Android, los `pom.xml` de Maven, los `.csproj` de .NET, los documentos de Office (`.docx` es un zip de XML) o los ficheros de configuración de casi cualquier herramienta.

Un ejemplo de cada uno, comprobado con un analizador real (todos están bien formados):

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100">
  <circle cx="50" cy="50" r="40" fill="orange"/>
</svg>
```

```xml
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi>x</mi><mo>+</mo><mn>1</mn>
</math>
```

```xml
<rss version="2.0">
  <channel>
    <title>Mi blog</title>
    <item><title>Primera entrada</title></item>
  </channel>
</rss>
```

```xml
<gml:Point xmlns:gml="http://www.opengis.net/gml" srsName="EPSG:4326">
  <gml:pos>40.4168 -3.7038</gml:pos>
</gml:Point>
```


## XML, HTML y JSON

| | XML | HTML | JSON |
|---|---|---|---|
| Para qué | Datos y documentos con estructura | Mostrar páginas web | Intercambiar datos entre programas |
| Etiquetas | Las defines tú | Un conjunto fijo | No tiene (usa `{"clave": valor}`) |
| Comprobar la estructura | Sí (DTD, XSD) | No | Con JSON Schema, aparte |
| Atributos y texto mezclado | Sí | Sí | No |
| Tamaño | El más voluminoso (etiqueta de cierre) | — | Más compacto |
| Se usa en | Configuración, documentos, SVG, RSS, SOAP | La web | APIs REST |

!!! tip "Cuándo elegir XML"
    Cuando el documento tiene **texto mezclado con marcas** (un libro, una página), cuando se necesita **validar** la estructura con un esquema o **transformarla** con XSLT, o cuando el formato ya lo exige (SVG, RSS, Android). Para APIs web sencillas, JSON suele bastar.

## Un documento completo

Esta es la biblioteca que usaremos como ejemplo en toda la web:

```xml
<?xml version="1.0" encoding="UTF-8"?>
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
</biblioteca>
```


Tiene un **prólogo** (la primera línea), un **comentario**, un elemento **raíz** (`biblioteca`) y tres elementos `libro` con **atributos** (`isbn`, `genero`) y **elementos hijos** (`titulo`, `autor`…). En el siguiente apartado se ve cada pieza.
