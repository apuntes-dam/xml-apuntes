# 3.1 XPath

**XPath** es un lenguaje para **seleccionar partes de un documento XML**: elementos, atributos o texto. Se parece a la ruta de un archivo (`/carpeta/archivo`), pero navega por el árbol del documento. Lo usan XSLT, XQuery, los validadores Schematron y casi todas las librerías de XML.

Todos los resultados de esta página son de la biblioteca de ejemplo de [1.1](../u01/01-que-es.md), evaluados con un motor XPath real.

## Rutas

| Símbolo | Significa |
|---|---|
| `/` | Desde la **raíz**, o paso de una ruta (`/a/b`: hijo `b` de `a`) |
| `//` | En **cualquier parte** del documento (descendientes) |
| `.` | El nodo actual |
| `..` | El padre del nodo actual |
| `@nombre` | Un **atributo** |
| `*` | Cualquier elemento |
| `text()` | El **texto** de un elemento |
| `[ ... ]` | Un **predicado**: filtra los nodos |
| `\|` | **Unión** de dos conjuntos de nodos |

## Ejemplos

| Expresión XPath | Qué selecciona | Resultado |
|---|---|---|
| `/biblioteca/libro/titulo` | Todos los títulos, desde la raíz | `<titulo>Cien años de soledad</titulo>` · `<titulo>El nombre de la rosa</titulo>` · `<titulo>Rayuela</titulo>` |
| `//autor` | Todos los `autor`, en cualquier parte | `<autor>Gabriel García Márquez</autor>` · `<autor>Umberto Eco</autor>` · `<autor>Julio Cortázar</autor>` |
| `/biblioteca/libro[1]/titulo/text()` | El texto del título del **primer** libro | `Cien años de soledad` |
| `/biblioteca/libro[last()]/titulo/text()` | El título del **último** libro | `Rayuela` |
| `//libro/@isbn` | Los atributos `isbn` de todos los libros | `978-84-376-0494-7` · `978-84-206-3365-1` · `978-84-663-1840-3` |
| `//libro[@genero='novela']/titulo/text()` | Títulos de las novelas | `Cien años de soledad` · `Rayuela` |
| `//libro[anio > 1970]/titulo/text()` | Libros posteriores a 1970 | `El nombre de la rosa` |
| `//libro[precio < 20]/titulo/text()` | Libros de menos de 20 euros | `Cien años de soledad` · `Rayuela` |
| `//titulo[contains(., 'rosa')]/text()` | Títulos que contienen «rosa» | `El nombre de la rosa` |
| `count(//libro)` | Cuántos libros hay | `3` |
| `sum(//precio)` | La suma de los precios | `61.4` |
| `//libro[2]/precio/@moneda` | La moneda del segundo libro | `EUR` |
| `//libro[titulo='Rayuela']/autor/text()` | El autor del libro «Rayuela» | `Julio Cortázar` |
| `//titulo/text() | //autor/text()` | Títulos **y** autores (unión) | `Cien años de soledad` · `Gabriel García Márquez` · `El nombre de la rosa` · `Umberto Eco` · `Rayuela` · `Julio Cortázar` |
| `name(/*)` | El nombre del elemento raíz | `biblioteca` |
### Predicados

Lo que va entre `[ ]` filtra:

* `[2]`: por **posición** (empieza en 1, no en 0), `[last()]` el último, `[position() < 3]` los dos primeros.
* `[@genero='novela']`: por **valor de atributo**.
* `[anio > 1970]`: por **valor de un hijo**; `[titulo='Rayuela']` compara su texto.
* `[contains(., 'rosa')]`: con funciones.

## Funciones útiles

| Función | Devuelve |
|---|---|
| `count(nodos)` | Cuántos nodos hay |
| `sum(nodos)` | La suma de sus valores numéricos |
| `contains(a, b)` / `starts-with(a, b)` | Si el texto `a` contiene / empieza por `b` |
| `string-length(x)` | Longitud del texto |
| `name(nodo)` | El nombre del elemento |
| `position()` / `last()` | La posición del nodo actual / la del último |
| `not(x)` / `and` / `or` | Lógica |

## Ejes

Además de bajar a los hijos, XPath puede moverse en otras direcciones con la sintaxis `eje::prueba`:

| Expresión | Qué hace | Resultado |
|---|---|---|
| `//titulo[.='Rayuela']/parent::libro/@isbn` | `parent::` sube al padre | `978-84-663-1840-3` |
| `//libro[1]/following-sibling::libro/titulo/text()` | `following-sibling::` los hermanos que van después | `El nombre de la rosa · Rayuela` |
| `//precio/ancestor::biblioteca/libro[1]/titulo/text()` | `ancestor::` los antecesores | `Cien años de soledad` |
| `//libro[autor='Umberto Eco']/descendant::anio/text()` | `descendant::` los descendientes | `1980` |
Los ejes más usados: `child::` (el normal, se puede omitir), `parent::`, `ancestor::`, `descendant::`, `following-sibling::`, `preceding-sibling::` y `attribute::` (`@`).

!!! warning "XPath 1.0"
    Las comprobaciones de esta web usan **XPath 1.0**, que es el que soportan los navegadores y casi todas las librerías. Las versiones 2.0 y 3.1 añaden más funciones y tipos, pero no son necesarias para empezar.
