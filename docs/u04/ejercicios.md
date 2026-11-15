# Ejercicios de la unidad 4

<div class="ej-gate" data-unit="u04" data-nombre="U4 · XML en la práctica"></div>

Escribe cada respuesta en un archivo `.xml` (o `.xsd`, `.xsl`) y **compruébala con un analizador**: ábrela en el navegador o en VS Code, o usa `xmllint` (ver [1.5](../u01/05-herramientas.md)). La solución modelo está bloqueada hasta que la unidad esté marcada como leída.

## Ejercicio 4.1

Escribe un **programa en Python** (con `xml.etree.ElementTree` y `json`) que lea esta tienda y la convierta en una **lista de diccionarios**, con las claves `nombre`, `categoria`, `precio` y `stock`. Imprímela con `json.dumps`, en **una sola línea y sin espacios** (`separators=(",", ":")`).

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
[{"nombre":"Agua","categoria":"bebida","precio":0.8,"stock":40},{"nombre":"Pan","categoria":"panaderia","precio":1.2,"stock":15},{"nombre":"Cola","categoria":"bebida","precio":1.5,"stock":0},{"nombre":"Manzanas","categoria":"fruta","precio":2.4,"stock":3},{"nombre":"Croissant","categoria":"panaderia","precio":1.8,"stock":8}]
```


<details class="sol" data-key="xml/4.1">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>from xml.etree import ElementTree as ET
import json
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.2

Al revés: a partir de esta lista de productos (en JSON) `[{"nombre": "Miel", "categoria": "despensa", "precio": 3.5, "stock": 6}, {"nombre": "Arroz", "categoria": "despensa", "precio": 1.1, "stock": 20}]`, genera el XML `<tienda>` con un `<producto categoria="...">` por cada uno, con `<nombre>`, `<precio>` y `<stock>` como **elementos hijos** (como en la tienda de los demás ejercicios), e imprímelo con `ET.tostring`.
**Salida esperada:**

```text
<tienda><producto categoria="despensa"><nombre>Miel</nombre><precio>3.5</precio><stock>6</stock></producto><producto categoria="despensa"><nombre>Arroz</nombre><precio>1.1</precio><stock>20</stock></producto></tienda>
```


<details class="sol" data-key="xml/4.2">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>from xml.etree import ElementTree as ET
productos = [
    {"nombre": "Miel", "categoria": "despensa", "precio": 3.5, "stock": 6},
    {"nombre": "Arroz", "categoria": "despensa", "precio": 1.1, "stock": 20},
]
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.3

Con la misma conversión a lista de diccionarios del ejercicio anterior, imprime en una línea cuántos productos tienen `stock` **mayor que 0** (`Con stock: N`) y, en otra, el `nombre` del producto más caro (`Más caro: nombre`).

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
Con stock: 4
Más caro: Manzanas
```


<details class="sol" data-key="xml/4.3">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>from xml.etree import ElementTree as ET
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Cola&lt;/nombre&gt;&lt;precio&gt;1.50&lt;/precio&gt;&lt;stock&gt;0&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.4

Escribe un manejador **SAX** (`xml.sax.ContentHandler`) que, para cada producto de esta tienda, imprima la línea `nombre: precio` **en cuanto termine de leer** su `<precio>` (sin esperar a que acabe el resto del `<producto>`).

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
Agua: 0.80
Pan: 1.20
Cola: 1.50
Manzanas: 2.40
Croissant: 1.80
```


<details class="sol" data-key="xml/4.4">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>import xml.sax
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Cola&lt;/nombre&gt;&lt;precio&gt;1.50&lt;/precio&gt;&lt;stock&gt;0&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.5

Escribe un manejador SAX que calcule el **stock total** de la tienda sin cargar el árbol entero, y al final imprima solo `Stock total: N`.

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
Stock total: 66
```


<details class="sol" data-key="xml/4.5">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>import xml.sax
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Cola&lt;/nombre&gt;&lt;precio&gt;1.50&lt;/precio&gt;&lt;stock&gt;0&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.6

Escribe un manejador SAX que cuente cuántos `<producto>` tienen el atributo `categoria="bebida"` (los atributos llegan ya en `startElement`), y al final imprima solo ese número.

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
2
```


<details class="sol" data-key="xml/4.6">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>import xml.sax
tienda = """&lt;tienda&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Agua&lt;/nombre&gt;&lt;precio&gt;0.80&lt;/precio&gt;&lt;stock&gt;40&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="panaderia"&gt;&lt;nombre&gt;Pan&lt;/nombre&gt;&lt;precio&gt;1.20&lt;/precio&gt;&lt;stock&gt;15&lt;/stock&gt;&lt;/producto&gt;
  &lt;producto categoria="bebida"&gt;&lt;nombre&gt;Cola&lt;/nombre&gt;&lt;precio&gt;1.50&lt;/precio&gt;&lt;stock&gt;0&lt;/stock&gt;&lt;/producto&gt;
# ... (resto de la solución bloqueado)</code></pre></div>
</details>

## Ejercicio 4.7

Con este catálogo:

```xml
<catalogo xmlns:lib="http://ejemplo.org/libros" xmlns:mus="http://ejemplo.org/musica">
  <lib:libro><lib:titulo>Rayuela</lib:titulo><lib:precio>17.00</lib:precio></lib:libro>
  <lib:libro><lib:titulo>Ficciones</lib:titulo><lib:precio>15.50</lib:precio></lib:libro>
  <mus:disco><mus:titulo>Kind of Blue</mus:titulo><mus:precio>12.00</mus:precio></mus:disco>
</catalogo>
```

Los **títulos** de los dos `lib:libro`. Escribe una **expresión XPath** (el prefijo que uses tiene que ir en el `ns` que le pases al motor XPath, igual que en 1.4 y 4.3).
**Resultado esperado:**

```text
Rayuela
Ficciones
```


<details class="sol" data-key="xml/4.7">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//lib:libro/lib:titulo/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 4.8

Con este catálogo:

```xml
<catalogo xmlns:lib="http://ejemplo.org/libros" xmlns:mus="http://ejemplo.org/musica">
  <lib:libro><lib:titulo>Rayuela</lib:titulo><lib:precio>17.00</lib:precio></lib:libro>
  <lib:libro><lib:titulo>Ficciones</lib:titulo><lib:precio>15.50</lib:precio></lib:libro>
  <mus:disco><mus:titulo>Kind of Blue</mus:titulo><mus:precio>12.00</mus:precio></mus:disco>
</catalogo>
```

El **título** del disco (vocabulario `mus`). Escribe una **expresión XPath** (el prefijo que uses tiene que ir en el `ns` que le pases al motor XPath, igual que en 1.4 y 4.3).
**Resultado esperado:**

```text
Kind of Blue
```


<details class="sol" data-key="xml/4.8">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>//mus:disco/mus:titulo/text()
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 4.9

Con este catálogo:

```xml
<catalogo xmlns:lib="http://ejemplo.org/libros" xmlns:mus="http://ejemplo.org/musica">
  <lib:libro><lib:titulo>Rayuela</lib:titulo><lib:precio>17.00</lib:precio></lib:libro>
  <lib:libro><lib:titulo>Ficciones</lib:titulo><lib:precio>15.50</lib:precio></lib:libro>
  <mus:disco><mus:titulo>Kind of Blue</mus:titulo><mus:precio>12.00</mus:precio></mus:disco>
</catalogo>
```

La **suma** de los precios de los libros (vocabulario `lib`). Escribe una **expresión XPath** (el prefijo que uses tiene que ir en el `ns` que le pases al motor XPath, igual que en 1.4 y 4.3).
**Resultado esperado:**

```text
32.5
```


<details class="sol" data-key="xml/4.9">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>sum(//lib:precio)
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>
