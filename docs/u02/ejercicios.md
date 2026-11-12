# Ejercicios de la unidad 2

<div class="ej-gate" data-unit="u02" data-nombre="U2 · Validación"></div>

Escribe cada respuesta en un archivo `.xml` (o `.xsd`, `.xsl`) y **compruébala con un analizador**: ábrela en el navegador o en VS Code, o usa `xmllint` (ver [1.5](../u01/05-herramientas.md)). La solución modelo está bloqueada hasta que la unidad esté marcada como leída.

## Ejercicio 2.1

Escribe una **DTD** para esta agenda: una `agenda` tiene **uno o más** `contacto`; cada contacto tiene un atributo `id` **obligatorio y único**, un `nombre`, **cero o más** `telefono` y **como mucho un** `email`.

```xml
<agenda>
  <contacto id="c1"><nombre>Marta</nombre><telefono>600111222</telefono><telefono>910333444</telefono><email>m@x.org</email></contacto>
  <contacto id="c2"><nombre>Pedro</nombre></contacto>
</agenda>
```


<details class="sol" data-key="xml/2.1">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;!DOCTYPE agenda [
  &lt;!ELEMENT agenda (contacto+)&gt;
  &lt;!ELEMENT contacto (nombre, telefono*, email?)&gt;
  &lt;!ATTLIST contacto id ID #REQUIRED&gt;
  &lt;!ELEMENT nombre (#PCDATA)&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.2

Escribe una **DTD** para un `pedido`: tiene un `cliente` y **una o más** `linea`; cada línea tiene `producto` y `cantidad`. El pedido lleva un atributo `estado` que solo puede valer `pendiente`, `enviado` o `entregado` (si falta, se toma `pendiente`).

```xml
<pedido estado="enviado">
  <cliente>Ana Ruiz</cliente>
  <linea><producto>Lápiz</producto><cantidad>10</cantidad></linea>
  <linea><producto>Cuaderno</producto><cantidad>2</cantidad></linea>
</pedido>
```


<details class="sol" data-key="xml/2.2">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;!DOCTYPE pedido [
  &lt;!ELEMENT pedido (cliente, linea+)&gt;
  &lt;!ATTLIST pedido estado (pendiente | enviado | entregado) "pendiente"&gt;
  &lt;!ELEMENT cliente (#PCDATA)&gt;
  &lt;!ELEMENT linea (producto, cantidad)&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.3

Escribe un **XSD** para este alumno: `nombre` (texto), `edad` (entero de 0 a 120), `email` (un texto con forma de correo: algo, `@`, algo, punto y al menos dos letras) y **una o más** `nota` (decimal de 0 a 10), en ese orden.

```xml
<alumno>
  <nombre>Lucía</nombre>
  <edad>19</edad>
  <email>lucia@ejemplo.org</email>
  <nota>8.5</nota>
  <nota>7</nota>
</alumno>
```


<details class="sol" data-key="xml/2.3">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="alumno"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.4

Escribe un **XSD** para un `producto` con `nombre` y `precio` (decimal **mayor que 0**). Lleva dos atributos **obligatorios**: `codigo` (tres letras mayúsculas, un guion y tres dígitos, como `ABC-123`) y `categoria` (solo `hogar`, `jardin` u `oficina`).

```xml
<producto codigo="ABC-123" categoria="hogar">
  <nombre>Lámpara</nombre>
  <precio>29.99</precio>
</producto>
```


<details class="sol" data-key="xml/2.4">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="producto"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.5

Escribe un **XSD** para un `evento`: un `titulo` (texto), una `fecha` (de tipo **fecha**, formato `aaaa-mm-dd`) y **un contacto, que puede ser un `telefono` o un `email`, pero no los dos**.

```xml
<evento><titulo>Jornada de puertas abiertas</titulo><fecha>2026-12-03</fecha><email>info@centro.org</email></evento>
```


<details class="sol" data-key="xml/2.5">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="evento"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.6

Traduce a **XSD** la DTD de la agenda del ejercicio 2.1 (`agenda`, `contacto` con `id` obligatorio y único, `nombre`, `telefono*` y `email?`). Fíjate en cómo se escriben `*`, `?` y `+` con `minOccurs` y `maxOccurs`.

<details class="sol" data-key="xml/2.6">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
  &lt;xs:element name="agenda"&gt;
    &lt;xs:complexType&gt;
      &lt;xs:sequence&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 2.7

Este documento está **bien formado** pero **no es válido** según el XSD del ejercicio 2.3. Encuentra **los dos errores** y corrígelo.

```xml
<alumno>
  <nombre>Lucía</nombre>
  <email>lucia@ejemplo.org</email>
  <edad>1900</edad>
  <nota>8.5</nota>
</alumno>
```


El validador dice (con el esquema de la solución del 2.3): **Element 'email': This element is not expected. Expected is ( edad ).**

<details class="sol" data-key="xml/2.7">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;alumno&gt;
  &lt;nombre&gt;Lucía&lt;/nombre&gt;
  &lt;edad&gt;19&lt;/edad&gt;
  &lt;email&gt;lucia@ejemplo.org&lt;/email&gt;
  &lt;nota&gt;8.5&lt;/nota&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>
