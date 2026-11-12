# 1.5 Herramientas

## Para escribir XML

| Herramienta | Qué ofrece |
|---|---|
| **Visual Studio Code** | Con la extensión *XML* de Red Hat: colores, cierre automático de etiquetas, sangría y avisos de buen formado y de validación |
| **IntelliJ IDEA / Android Studio** | Edición de XML con validación y ayuda con los vocabularios que conoce (Android, Maven, Spring…) |
| **Un navegador** | Abre un `.xml` y lo muestra como árbol; si está mal formado, enseña el error y la posición |
| **Un editor de texto** | XML es texto: sirve cualquiera (guarda siempre en **UTF-8**) |

## Para comprobarlo desde la consola

```bash
xmllint --noout biblioteca.xml                          # ¿está bien formado? (no escribe nada si lo está)
xmllint --noout --dtdvalid biblioteca.dtd biblioteca.xml    # validar con una DTD
xmllint --noout --schema biblioteca.xsd biblioteca.xml      # validar con un XSD
xmllint --xpath "//libro/titulo/text()" biblioteca.xml      # lanzar una consulta XPath
```

`xmllint` (de la librería libxml2) viene en Linux y macOS, y se instala en Windows con los binarios de libxml2. Las comprobaciones de esta web se hacen con la misma librería a través de Python (`lxml`).

## Desde un programa

Cada lenguaje trae su analizador: Python (`xml.etree.ElementTree`, `lxml`), Java (`DocumentBuilder`), C# (`System.Xml.Linq`)… Se ven en [3.3](../u03/03-programas.md). Un ejemplo mínimo de comprobación de buen formado en Python:

```python
from xml.etree import ElementTree as ET

for doc in ("<a><b>hola</b></a>", "<a><b>hola</a>"):
    try:
        ET.fromstring(doc)
        print(doc, "-> bien formado")
    except ET.ParseError as e:
        print(doc, "-> mal formado:", e)
```

**Salida:**

```text
<a><b>hola</b></a> -> bien formado
<a><b>hola</a> -> mal formado: mismatched tag: line 1, column 12
```

!!! note "Codificación"
    Si el prólogo dice `encoding="UTF-8"` (o no dice nada, que es lo mismo), el archivo **debe estar guardado en UTF-8**. Si lo guardas en otra codificación y pones tildes, el analizador da un error de caracteres no válidos.
