# 3.2 XSLT

**XSLT** (*eXtensible Stylesheet Language Transformations*) es un lenguaje, escrito en XML, que **transforma un documento XML en otro** documento: otro XML con otra estructura, una página HTML o un texto. Una **hoja de estilos XSLT** es un conjunto de **plantillas**: cada una dice «cuando encuentres esta parte del documento, produce esto».

Se aplica con un **procesador XSLT** (en el navegador, en `xsltproc`, en Java, en Python con `lxml`…). Las transformaciones de esta página las ha hecho uno real (XSLT 1.0).

## La estructura de una hoja

```xml
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="html"/>          <!-- el tipo de resultado: xml, html o text -->
  <xsl:template match="/biblioteca">   <!-- una plantilla: a qué parte se aplica (XPath) -->
    … lo que se escribe …
  </xsl:template>
</xsl:stylesheet>
```

## Las instrucciones principales

| Instrucción | Qué hace |
|---|---|
| `xsl:template match="…"` | Define una plantilla para los nodos que cumplan ese XPath |
| `xsl:value-of select="…"` | Escribe el **valor** (texto) de lo que selecciona el XPath |
| `xsl:for-each select="…"` | **Repite** el bloque por cada nodo seleccionado |
| `xsl:apply-templates select="…"` | Aplica a esos nodos **las plantillas** que les correspondan |
| `xsl:sort select="…"` | **Ordena** (dentro de `for-each`), con `data-type="number"` para números |
| `xsl:if test="…"` | Se ejecuta **si** se cumple la condición |
| `xsl:choose` / `xsl:when` / `xsl:otherwise` | Varias condiciones (un `if / else if / else`) |
| `xsl:text` | Escribe un texto literal (para espacios y saltos de línea) |
| `{expresión}` en un atributo | Escribe el valor de una expresión dentro de un **atributo** del resultado |

## Ejemplo 1: de XML a una tabla HTML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="html" indent="yes"/>

  <xsl:template match="/biblioteca">
    <table border="1">
      <tr><th>Título</th><th>Autor</th><th>Precio</th></tr>
      <xsl:for-each select="libro">
        <xsl:sort select="precio" data-type="number"/>
        <tr>
          <td><xsl:value-of select="titulo"/></td>
          <td><xsl:value-of select="autor"/></td>
          <td><xsl:value-of select="precio"/><xsl:text> </xsl:text><xsl:value-of select="precio/@moneda"/></td>
        </tr>
      </xsl:for-each>
    </table>
  </xsl:template>
</xsl:stylesheet>
```

Aplicada a la biblioteca (con los libros **ordenados por precio**), da:

```xml
<table border="1">
<tr>
<th>Título</th>
<th>Autor</th>
<th>Precio</th>
</tr>
<tr>
<td>Rayuela</td>
<td>Julio Cortázar</td>
<td>17.00 EUR</td>
</tr>
<tr>
<td>Cien años de soledad</td>
<td>Gabriel García Márquez</td>
<td>19.90 EUR</td>
</tr>
<tr>
<td>El nombre de la rosa</td>
<td>Umberto Eco</td>
<td>24.50 EUR</td>
</tr>
</table>
```

## Ejemplo 2: de XML a texto

Con `xsl:apply-templates` el trabajo se reparte: la plantilla de la raíz recorre los libros y la de `libro` escribe cada uno. El `xsl:if` añade «[oferta]» a los baratos.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="text"/>

  <xsl:template match="/biblioteca">
    <xsl:text>Catálogo (</xsl:text><xsl:value-of select="count(libro)"/><xsl:text> libros)&#10;</xsl:text>
    <xsl:apply-templates select="libro"/>
  </xsl:template>

  <xsl:template match="libro">
    <xsl:text>- </xsl:text><xsl:value-of select="titulo"/>
    <xsl:text> (</xsl:text><xsl:value-of select="anio"/><xsl:text>)</xsl:text>
    <xsl:if test="precio &lt; 20"><xsl:text> [oferta]</xsl:text></xsl:if>
    <xsl:text>&#10;</xsl:text>
  </xsl:template>
</xsl:stylesheet>
```

**Resultado:**

```text
Catálogo (3 libros)
- Cien años de soledad (1967) [oferta]
- El nombre de la rosa (1980)
- Rayuela (1963) [oferta]
```

## Ejemplo 3: de XML a otro XML

Con `{@isbn}` el valor de un atributo del origen pasa a un atributo del resultado:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="xml" indent="yes"/>

  <xsl:template match="/biblioteca">
    <catalogo>
      <xsl:for-each select="libro">
        <obra codigo="{@isbn}" tipo="{@genero}">
          <xsl:value-of select="titulo"/>
        </obra>
      </xsl:for-each>
    </catalogo>
  </xsl:template>
</xsl:stylesheet>
```

```xml
<?xml version="1.0"?>
<catalogo>
  <obra codigo="978-84-376-0494-7" tipo="novela">Cien años de soledad</obra>
  <obra codigo="978-84-206-3365-1" tipo="ensayo">El nombre de la rosa</obra>
  <obra codigo="978-84-663-1840-3" tipo="novela">Rayuela</obra>
</catalogo>
```

!!! info "Dónde se usa XSLT"
    Para convertir datos XML en páginas web, en informes, en otro formato de intercambio, o para **migrar** documentos de una estructura a otra. Un documento puede incluir `<?xml-stylesheet type="text/xsl" href="estilo.xsl"?>` para que el navegador lo transforme al abrirlo.
