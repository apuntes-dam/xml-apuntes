# 1.2 La estructura de un documento

## Las piezas

```xml
<?xml version="1.0" encoding="UTF-8"?>      <!-- 1. prólogo -->
<!-- un comentario -->                       <!-- 2. comentario -->
<libro isbn="978-84-376-0494-7">             <!-- 3. elemento raíz, con un atributo -->
  <titulo>Rayuela</titulo>                   <!-- 4. elemento con texto -->
  <portada/>                                 <!-- 5. elemento vacío -->
</libro>
```

| Pieza | Qué es | Reglas |
|---|---|---|
| **Prólogo** (declaración XML) | `<?xml version="1.0" encoding="UTF-8"?>`: versión y codificación | Opcional, pero si está debe ser **lo primero** del archivo (ni un espacio antes) |
| **Elemento** | `<titulo>…</titulo>`: etiqueta de apertura, contenido y etiqueta de cierre | Todo elemento abierto se **cierra**; los vacíos se pueden escribir `<portada/>` |
| **Elemento raíz** | El que contiene a todos los demás | Solo **uno** por documento |
| **Atributo** | `isbn="…"`: un dato sobre el elemento, dentro de la etiqueta de apertura | Valor **siempre entre comillas** (simples o dobles); no se repite en un mismo elemento |
| **Texto** | El contenido entre etiquetas | Los caracteres `<` y `&` hay que escribirlos con entidades |
| **Comentario** | `<!-- … -->` | No puede contener `--` dentro ni ir antes del prólogo |
| **Instrucción de procesamiento** | `<?xml-stylesheet href="estilo.xsl" type="text/xsl"?>` | Pasa información a la aplicación que lee el documento |

!!! note "Mayúsculas y minúsculas"
    XML **distingue mayúsculas de minúsculas**: `<Libro>` y `<libro>` son etiquetas distintas, y `</LIBRO>` no cierra a `<libro>`.

## Nombres de elementos y atributos

Pueden llevar letras (también acentuadas), dígitos, guion, guion bajo y punto, pero **no pueden empezar por un dígito** ni contener espacios, y no deben empezar por `xml` (está reservado). Son válidos `precio`, `fecha_alta`, `año`; no lo son `2oferta` ni `fecha alta`.

## Elemento o atributo

Para el mismo dato hay dos formas:

```xml
<libro isbn="978-84-376-0494-7"><titulo>Rayuela</titulo></libro>     <!-- isbn como atributo -->
<libro><isbn>978-84-376-0494-7</isbn><titulo>Rayuela</titulo></libro> <!-- isbn como elemento -->
```

Regla práctica: el **atributo** para datos **simples** que identifican o describen (un identificador, una unidad, un estado) y el **elemento** para lo que tiene **estructura o puede repetirse** (varios autores, un texto largo). Un atributo no puede tener hijos ni repetirse.

## Caracteres especiales: entidades

Cinco caracteres tienen un significado en XML y se escriben con una **entidad**:

| Carácter | Entidad | Ejemplo |
|---|---|---|
| `<` | `&lt;` | `5 &lt; 6` |
| `>` | `&gt;` | `7 &gt; 3` |
| `&` | `&amp;` | `Tom &amp; Jerry` |
| `'` | `&apos;` | `l&apos;eau` |
| `"` | `&quot;` | `&quot;hola&quot;` |

```xml
<texto>5 &lt; 6 y Tom &amp; Jerry &#169; &#x20AC;</texto>
```

Una **referencia numérica** (`&#169;`, `&#x20AC;`) inserta cualquier carácter Unicode por su número. Con el resultado real: **El texto que lee el programa:**

```text
5 < 6 y Tom & Jerry © €
```


!!! warning "`&nbsp;` no existe en XML"
    Las entidades de HTML como `&nbsp;`, `&eacute;` o `&copy;` **no están definidas** en XML y dan un error (`Entity 'nbsp' not defined`). Escribe el carácter directamente (UTF-8) o su referencia numérica (`&#160;`).

## Secciones CDATA

Cuando un bloque tiene muchos `<` o `&` (código, fórmulas), se puede escribir **tal cual** dentro de una sección `CDATA`:

```xml
<codigo><![CDATA[ if (a < b && b > 0) { ok(); } ]]></codigo>
```

Dentro de `<![CDATA[ … ]]>` nada se interpreta como etiqueta: el texto que lee el programa es exactamente lo escrito. Lo único que no puede aparecer dentro es la secuencia `]]>`.

## Leer la estructura

El analizador ve el documento como un **árbol**: la raíz arriba, y de ella cuelgan los hijos. En la biblioteca de ejemplo, el analizador cuenta **3** libros y sus títulos son:

**Títulos (XPath /biblioteca/libro/titulo/text()):**

```text
Cien años de soledad
El nombre de la rosa
Rayuela
```

Los **espacios y saltos de línea** entre etiquetas (la sangría) también son texto, pero un programa los suele ignorar.
