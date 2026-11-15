# 4.3 Consultar documentos con espacios de nombres

[1.4](../u01/04-espacios.md) explicó qué es un espacio de nombres y [3.1](../u03/01-xpath.md) cómo consultar un documento con XPath; aquí se juntan las dos cosas, porque es donde más gente se atasca.

## El documento

```xml
<html xmlns="http://www.w3.org/1999/xhtml">
  <body>
    <h1>Mi icono</h1>
    <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60">
      <circle cx="30" cy="30" r="25" fill="orange"/>
    </svg>
  </body>
</html>
```


`<h1>` no lleva prefijo, pero **sí** pertenece a un espacio de nombres: el `xmlns` de `<html>` es el espacio **por defecto**, y afecta a todo lo que hay dentro (igual que en 1.4). `<circle>` tampoco lleva prefijo, y pertenece al espacio de SVG por el mismo motivo.

## La trampa: una consulta sin espacio de nombres

**Resultado de //circle:**

```text
(nada)
```

**Resultado de //h1/text():**

```text
(nada)
```

Las dos consultas devuelven **nada**, aunque las etiquetas existen y se ven en el documento. En XPath, un nombre sin prefijo (`circle`, `h1`) solo encaja con un elemento que **no tiene** espacio de nombres — y aquí los dos lo tienen, aunque no se note al mirar las etiquetas.

## El arreglo: decirle a XPath qué prefijo es qué dirección

Se le pasa a la consulta un mapa de prefijo → dirección (el prefijo lo eliges tú, la dirección tiene que ser exactamente la del `xmlns`):

**Resultado de //s:circle con el prefijo s -> espacio de SVG:**

```text
<circle xmlns="http://www.w3.org/2000/svg" cx="30" cy="30" r="25" fill="orange"/>
```

**Resultado de //x:h1/text() con el prefijo x -> espacio de XHTML:**

```text
Mi icono
```

!!! warning "El error más típico con namespaces"
    Una consulta que «debería» encontrar algo y devuelve una lista vacía, sin ningún error, es casi siempre esto: el documento tiene un espacio de nombres (por defecto o con prefijo) que la consulta no está teniendo en cuenta.
