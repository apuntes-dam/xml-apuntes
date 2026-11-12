# Ejercicios de la unidad 1

<div class="ej-gate" data-unit="u01" data-nombre="U1 · Documentos XML"></div>

Escribe cada respuesta en un archivo `.xml` (o `.xsd`, `.xsl`) y **compruébala con un analizador**: ábrela en el navegador o en VS Code, o usa `xmllint` (ver [1.5](../u01/05-herramientas.md)). La solución modelo está bloqueada hasta que la unidad esté marcada como leída.

## Ejercicio 1.1

Este documento **no está bien formado**. Encuentra los **tres errores** y escríbelo bien:

```xml
<?xml version="1.0"?>
<pedido num=15>
  <cliente>Ana & Luis</cliente>
  <articulo>Lápiz</Articulo>
</pedido>
```


<details class="sol" data-key="xml/1.1">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0"?&gt;
&lt;pedido num="15"&gt;
  &lt;cliente&gt;Ana &amp;amp; Luis&lt;/cliente&gt;
  &lt;articulo&gt;Lápiz&lt;/articulo&gt;
&lt;/pedido&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.2

Escribe un documento XML de un **alumno** con un atributo `id`, los elementos `nombre` y `apellidos` y **tres** elementos `nota`, cada uno con un atributo `asignatura`.

<details class="sol" data-key="xml/1.2">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;alumno id="A-001"&gt;
  &lt;nombre&gt;Lucía&lt;/nombre&gt;
  &lt;apellidos&gt;Ramos Díaz&lt;/apellidos&gt;
  &lt;nota asignatura="Programación"&gt;8.5&lt;/nota&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.3

Escribe el texto `Si a < b && c > d, usa 'x' y "y"` dentro de un elemento `<regla>` **de dos formas**: usando **entidades** y usando una sección **CDATA**. Las dos deben dar el mismo texto.

<details class="sol" data-key="xml/1.3">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;!-- con entidades --&gt;
&lt;regla&gt;Si a &amp;lt; b &amp;amp;&amp;amp; c &amp;gt; d, usa 'x' y "y"&lt;/regla&gt;
&lt;!-- con CDATA --&gt;
&lt;regla&gt;&lt;![CDATA[Si a &lt; b &amp;&amp; c &gt; d, usa 'x' y "y"]]&gt;&lt;/regla&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.4

Escribe una **agenda** con dos contactos. Cada contacto tiene un atributo `id` y un `nombre`; el primero tiene **dos teléfonos** (con un atributo `tipo`) y un `email`, y el segundo **un solo teléfono** y ningún email.

<details class="sol" data-key="xml/1.4">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;agenda&gt;
  &lt;contacto id="1"&gt;
    &lt;nombre&gt;Marta Gil&lt;/nombre&gt;
    &lt;telefono tipo="móvil"&gt;600111222&lt;/telefono&gt;
    &lt;telefono tipo="casa"&gt;910333444&lt;/telefono&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.5

Escribe una página **XHTML** (con un párrafo) que contenga, dentro del `body`, un dibujo **SVG** con un rectángulo (`rect`). Declara bien los dos **espacios de nombres**.

<details class="sol" data-key="xml/1.5">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
  &lt;body&gt;
    &lt;p&gt;Un rectángulo azul:&lt;/p&gt;
    &lt;svg xmlns="http://www.w3.org/2000/svg" width="80" height="40"&gt;
      &lt;rect width="80" height="40" fill="blue"/&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.6

Un documento mezcla dos vocabularios: el de **libros** (`http://ejemplo.org/libros`) y el de **autores** (`http://ejemplo.org/autores`), y ambos tienen un elemento `nombre`. Escribe un documento con el título de un libro y el nombre de su autor sin que los `nombre` choquen, usando **prefijos**.

<details class="sol" data-key="xml/1.6">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;recursos xmlns:lib="http://ejemplo.org/libros" xmlns:aut="http://ejemplo.org/autores"&gt;
  &lt;lib:nombre&gt;Rayuela&lt;/lib:nombre&gt;
  &lt;aut:nombre&gt;Julio Cortázar&lt;/aut:nombre&gt;
&lt;/recursos&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.7

Escribe una `compra` con dos `producto` que lleve, **antes** de la raíz, una instrucción de procesamiento que enlace la hoja de estilos `estilo.xsl` (`type="text/xsl"`) y un **comentario**.

<details class="sol" data-key="xml/1.7">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;?xml-stylesheet type="text/xsl" href="estilo.xsl"?&gt;
&lt;!-- Lista de la compra --&gt;
&lt;compra&gt;
  &lt;producto&gt;Leche&lt;/producto&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>

## Ejercicio 1.8

Modela una **receta** con nombre y número de raciones, tres **ingredientes** (cada uno con cantidad y unidad) y los **pasos** en orden. Decide qué va como **atributo** y qué como **elemento**: los datos simples que describen, en atributos; lo que se repite o tiene estructura, en elementos.

<details class="sol" data-key="xml/1.8">
<summary>Solución modelo (bloqueada)</summary>
<div class="sol-body"><p class="sol-aviso">🔒 La solución completa está bloqueada. Esto es solo un ejemplo de cómo empieza:</p><pre><code>&lt;receta nombre="Tortilla de patatas" raciones="4"&gt;
  &lt;ingrediente cantidad="6" unidad="unidades"&gt;huevo&lt;/ingrediente&gt;
  &lt;ingrediente cantidad="500" unidad="g"&gt;patata&lt;/ingrediente&gt;
  &lt;ingrediente cantidad="1" unidad="unidad"&gt;cebolla&lt;/ingrediente&gt;
  &lt;pasos&gt;
&lt;!-- ... (resto de la solución bloqueado) --&gt;</code></pre></div>
</details>
