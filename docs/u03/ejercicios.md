# Ejercicios de la unidad 3

<div class="ej-gate" data-unit="u03" data-nombre="U3 · Consultar y transformar"></div>

Escribe cada respuesta en un archivo `.xml` (o `.xsd`, `.xsl`) y **compruébala con un analizador**: ábrela en el navegador o en VS Code, o usa `xmllint` (ver [1.5](../u01/05-herramientas.md)). La solución modelo está bloqueada hasta que la unidad esté marcada como leída.

## Ejercicio 3.1

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Los **nombres** de los productos de la categoría `bebida`. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
Agua
Cola
```


<details class="sol" data-key="xml/3.1">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//producto[@categoria='bebida']/nombre/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.2

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

**Cuántos** productos tienen `stock` igual a 0. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
1
```


<details class="sol" data-key="xml/3.2">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>count(//producto[stock=0])
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.3

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

El `nombre` del **segundo** producto. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
Pan
```


<details class="sol" data-key="xml/3.3">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>/tienda/producto[2]/nombre/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.4

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

El valor del atributo `categoria` del producto llamado `Manzanas`. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
fruta
```


<details class="sol" data-key="xml/3.4">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//producto[nombre='Manzanas']/@categoria
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.5

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Los nombres de los productos que cuestan **más de 1,50**. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
Manzanas
Croissant
```


<details class="sol" data-key="xml/3.5">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//producto[precio &gt; 1.5]/nombre/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.6

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Los nombres que **empiezan por `C`**. Escribe una **expresión XPath**.
**Resultado esperado:**

```text
Cola
Croissant
```


<details class="sol" data-key="xml/3.6">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//producto[starts-with(nombre, 'C')]/nombre/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.7

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

El `nombre` del producto **más caro** (XPath 1.0 no tiene `max`: piensa en «el que no tiene ninguno más caro»). Escribe una **expresión XPath**.
**Resultado esperado:**

```text
Manzanas
```


<details class="sol" data-key="xml/3.7">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//producto[not(precio &lt; //producto/precio)]/nombre/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.8

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Escribe una **hoja XSLT** que produzca **texto** con una línea `nombre: precio` por producto, **ordenados de más caro a más barato**.
**Resultado esperado:**

```text
Manzanas: 2.40
Croissant: 1.80
Cola: 1.50
Pan: 1.20
Agua: 0.80
```


<details class="sol" data-key="xml/3.8">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"&gt;
  &lt;xsl:output method="text"/&gt;
  &lt;xsl:template match="/tienda"&gt;
    &lt;xsl:for-each select="producto"&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.9

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Escribe una **hoja XSLT** que dé, por producto, una línea `nombre: estado` donde el estado es `agotado` si el `stock` es 0, `pocas unidades` si es menor que 5 y `disponible` en otro caso (usa `xsl:choose`).
**Resultado esperado:**

```text
Agua: disponible
Pan: disponible
Cola: agotado
Manzanas: pocas unidades
Croissant: disponible
```


<details class="sol" data-key="xml/3.9">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"&gt;
  &lt;xsl:output method="text"/&gt;
  &lt;xsl:template match="/tienda"&gt;
    &lt;xsl:for-each select="producto"&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.10

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Escribe una **hoja XSLT** que genere una lista HTML `<ul>` con un `<li>` del tipo `Agua (bebida)` para los productos de las categorías `bebida` y `fruta`.
**Resultado esperado:**

```text
<ul><li>Agua (bebida)</li><li>Cola (bebida)</li><li>Manzanas (fruta)</li></ul>
```


<details class="sol" data-key="xml/3.10">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"&gt;
  &lt;xsl:output method="html" indent="no"/&gt;
  &lt;xsl:template match="/tienda"&gt;
    &lt;ul&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.11

Con esta tienda:

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

Escribe una **hoja XSLT** que transforme la tienda en otro XML: la raíz `inventario` con un elemento `item` por producto, que tenga los **atributos** `nombre` y `categoria` y como **texto** el `stock` (por ejemplo `<item nombre="Agua" categoria="bebida">40</item>`).
**Resultado esperado:**

```text
<inventario><item nombre="Agua" categoria="bebida">40</item><item nombre="Pan" categoria="panaderia">15</item><item nombre="Cola" categoria="bebida">0</item><item nombre="Manzanas" categoria="fruta">3</item><item nombre="Croissant" categoria="panaderia">8</item></inventario>
```


<details class="sol" data-key="xml/3.11">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"&gt;
  &lt;xsl:output method="xml" omit-xml-declaration="yes" indent="no"/&gt;
  &lt;xsl:template match="/tienda"&gt;
    &lt;inventario&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 3.12

Escribe un **programa en Python** (con `xml.etree.ElementTree`) que lea esta tienda, muestre por cada producto `nombre valor` (donde `valor` es `precio × stock`, redondeado a 2 decimales) y al final `Total del inventario: X`.

```xml
<tienda>
  <producto categoria="bebida"><nombre>Agua</nombre><precio>0.80</precio><stock>40</stock></producto>
  <producto categoria="panaderia"><nombre>Pan</nombre><precio>1.20</precio><stock>15</stock></producto>
  <producto categoria="bebida"><nombre>Cola</nombre><precio>1.50</precio><stock>0</stock></producto>
  <producto categoria="fruta"><nombre>Manzanas</nombre><precio>2.40</precio><stock>3</stock></producto>
  <producto categoria="panaderia"><nombre>Croissant</nombre><precio>1.80</precio><stock>8</stock></producto>
</tienda>
```

**Salida esperada:**

```text
Agua 32.0
Pan 18.0
Cola 0.0
Manzanas 7.2
Croissant 14.4
Total del inventario: 71.6
```


<details class="sol" data-key="xml/3.12">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>from xml.etree import ElementTree as ET
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Cola&lt;/nombre&gt;&lt;precio&gt;1.50&lt;/precio&gt;&lt;stock&gt;0&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>
