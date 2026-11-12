# 1.4 Espacios de nombres

## El problema

Si en un mismo documento mezclas vocabularios distintos, los nombres pueden **chocar**: un `<titulo>` de un libro y un `<titulo>` de un disco. Un **espacio de nombres** (*namespace*) es una «dirección» que identifica a qué vocabulario pertenece cada etiqueta.

## Forma 1: un espacio por defecto

Con `xmlns="…"` todos los elementos de ese bloque (sin prefijo) pasan a pertenecer al vocabulario. Así se mezcla SVG dentro de XHTML:

```xml
<html xmlns="http://www.w3.org/1999/xhtml">
  <body>
    <p>Un círculo:</p>
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60">
      <circle cx="30" cy="30" r="25"/>
    </svg>
  </body>
</html>
```

`<html>` pertenece a XHTML y `<svg>` y `<circle>` a SVG, aunque no lleven prefijo, porque cada `xmlns` afecta a **su elemento y a todo lo que contiene**.

## Forma 2: con prefijos

Se declara un prefijo con `xmlns:prefijo="…"` y se escribe delante del nombre:

```xml
<catalogo xmlns:lib="http://ejemplo.org/libros" xmlns:mus="http://ejemplo.org/musica">
  <lib:titulo>Rayuela</lib:titulo>
  <mus:titulo>Kind of Blue</mus:titulo>
</catalogo>
```

Los dos `titulo` ya no chocan: uno es `lib:titulo` y el otro `mus:titulo`.

!!! info "La dirección no se visita"
    `http://ejemplo.org/libros` **no es una página web a la que se acceda**: es solo un identificador único (por eso suele ser una URL, para que no se repita). Lo que importa es que sea **igual** en todos los sitios que usan ese vocabulario.

## Consultar un documento con espacios de nombres

Hay que decirle al analizador qué prefijo corresponde a qué dirección. Con XPath (ver [3.1](../u03/01-xpath.md)) en el documento anterior:

**Resultado de /catalogo/lib:titulo/text():**

```text
Rayuela
```

El prefijo de la consulta puede ser **cualquiera** (`l`, `libros`…): importa la **dirección**, no el prefijo con el que se escribió el documento.
