# 3.3 XML desde un programa

Casi todos los lenguajes traen un **analizador de XML**. Hay dos formas de leer un documento:

| Modelo | Cómo funciona | Cuándo |
|---|---|---|
| **DOM** (*Document Object Model*) | Carga **todo el documento en memoria** como un árbol y se navega y modifica | Documentos pequeños o medianos; es lo más cómodo |
| **SAX / de flujo** | Recorre el documento **de principio a fin** avisando de cada etiqueta, sin guardarlo entero | Documentos enormes o cuando solo se lee una vez |

El mismo ejemplo, en tres lenguajes: leer una biblioteca, sumar los precios y buscar los ISBN de las novelas. Los tres programas se han **ejecutado** al generar esta página.

## Python (`xml.etree.ElementTree`)

```python
from xml.etree import ElementTree as ET

xml = """<biblioteca>
  <libro isbn="A1" genero="novela"><titulo>Rayuela</titulo><precio>17.00</precio></libro>
  <libro isbn="A2" genero="ensayo"><titulo>El nombre de la rosa</titulo><precio>24.50</precio></libro>
</biblioteca>"""

raiz = ET.fromstring(xml)
for libro in raiz.findall("libro"):
    print(libro.get("isbn"), libro.find("titulo").text, float(libro.find("precio").text))

total = sum(float(p.text) for p in raiz.iter("precio"))
print("Total:", total)
print([l.get("isbn") for l in raiz.findall("libro[@genero='novela']")])

nuevo = ET.SubElement(raiz, "libro", isbn="A3")
ET.SubElement(nuevo, "titulo").text = "Ficciones"
print(ET.tostring(nuevo, encoding="unicode"))
```

**Salida:**

```text
A1 Rayuela 17.0
A2 El nombre de la rosa 24.5
Total: 41.5
['A1']
<libro isbn="A3"><titulo>Ficciones</titulo></libro>
```

`find` y `findall` aceptan una versión reducida de XPath (rutas y predicados simples); la librería `lxml` ofrece XPath completo, XSLT y validación con DTD y XSD.

## Java (DOM y XPath)

```java
import java.io.StringReader;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.xpath.XPathFactory;
import org.w3c.dom.*;
import org.xml.sax.InputSource;

public class LeerXml {
    public static void main(String[] args) throws Exception {
        String xml = "<biblioteca>"
            + "<libro isbn=\"A1\" genero=\"novela\"><titulo>Rayuela</titulo><precio>17.00</precio></libro>"
            + "<libro isbn=\"A2\" genero=\"ensayo\"><titulo>El nombre de la rosa</titulo><precio>24.50</precio></libro>"
            + "</biblioteca>";
        Document doc = DocumentBuilderFactory.newInstance().newDocumentBuilder()
                .parse(new InputSource(new StringReader(xml)));
        NodeList libros = doc.getElementsByTagName("libro");
        double total = 0;
        for (int i = 0; i < libros.getLength(); i++) {
            Element libro = (Element) libros.item(i);
            String titulo = libro.getElementsByTagName("titulo").item(0).getTextContent();
            double precio = Double.parseDouble(libro.getElementsByTagName("precio").item(0).getTextContent());
            System.out.println(libro.getAttribute("isbn") + " " + titulo + " " + precio);
            total += precio;
        }
        System.out.println("Total: " + total);
        System.out.println(XPathFactory.newInstance().newXPath()
                .evaluate("//libro[@genero='novela']/@isbn", doc));
    }
}
```

**Salida:**

```text
A1 Rayuela 17.0
A2 El nombre de la rosa 24.5
Total: 41.5
A1
```

## C# (`System.Xml.Linq`, LINQ to XML)

```csharp
using System.Xml.Linq;

var doc = XDocument.Parse("""
<biblioteca>
  <libro isbn="A1" genero="novela"><titulo>Rayuela</titulo><precio>17.00</precio></libro>
  <libro isbn="A2" genero="ensayo"><titulo>El nombre de la rosa</titulo><precio>24.50</precio></libro>
</biblioteca>
""");

foreach (var libro in doc.Root!.Elements("libro"))
{
    Console.WriteLine($"{libro.Attribute("isbn")!.Value} {libro.Element("titulo")!.Value}");
}

var total = doc.Descendants("precio").Sum(p => double.Parse(p.Value, System.Globalization.CultureInfo.InvariantCulture));
Console.WriteLine($"Total: {total}");
Console.WriteLine(doc.Root.Elements("libro").Where(l => (string?)l.Attribute("genero") == "novela").Select(l => (string?)l.Attribute("isbn")).First());
```

**Salida:**

```text
A1 Rayuela
A2 El nombre de la rosa
Total: 41,5
A1
```

## Resumen

| Tarea | Python | Java | C# |
|---|---|---|---|
| Leer un texto XML | `ET.fromstring` | `DocumentBuilder.parse` | `XDocument.Parse` |
| Hijos por nombre | `findall("libro")` | `getElementsByTagName` | `Elements("libro")` |
| Leer un atributo | `.get("isbn")` | `.getAttribute("isbn")` | `.Attribute("isbn")` |
| Leer el texto | `.text` | `.getTextContent()` | `.Value` |
| XPath | `findall` (básico), `lxml` (completo) | `XPathFactory` | `XPathSelectElements` |

!!! note "Decimales"
    El texto de un número en XML siempre lleva punto (`17.00`). En C#, `double.Parse` usa el idioma del equipo: por eso se pasa `CultureInfo.InvariantCulture` (ver la [web de C#](https://apuntes-dam.github.io/csharp-apuntes/)).
