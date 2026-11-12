# 2.2 DTD

Una **DTD** (*Document Type Definition*) describe qué elementos y atributos puede tener un documento y en qué orden. Se escribe con una sintaxis propia (no es XML) y puede ir **dentro** del documento o en un **archivo aparte**.

## Dónde va

```xml
<!DOCTYPE biblioteca [ … declaraciones … ]>          <!-- interna: dentro del documento -->
<!DOCTYPE biblioteca SYSTEM "biblioteca.dtd">        <!-- externa: en un archivo aparte -->
```

El `DOCTYPE` va **después del prólogo y antes del elemento raíz**, y su nombre es el del elemento raíz.

## La DTD de la biblioteca

```xml
<!DOCTYPE biblioteca [
  <!ELEMENT biblioteca (libro+)>
  <!ELEMENT libro (titulo, autor+, anio, precio)>
  <!ATTLIST libro isbn CDATA #REQUIRED
                  genero (novela | ensayo | poesia) "novela">
  <!ELEMENT titulo (#PCDATA)>
  <!ELEMENT autor  (#PCDATA)>
  <!ELEMENT anio   (#PCDATA)>
  <!ELEMENT precio (#PCDATA)>
  <!ATTLIST precio moneda CDATA #FIXED "EUR">
]>
```

Y con ella, el documento de ejemplo es **válido**: el validador no da ningún error.

## Elementos: `<!ELEMENT nombre contenido>`

| Contenido | Significa | Ejemplo |
|---|---|---|
| `(#PCDATA)` | Solo texto | `<!ELEMENT titulo (#PCDATA)>` |
| `EMPTY` | Vacío (puede tener atributos) | `<!ELEMENT portada EMPTY>` |
| `ANY` | Cualquier contenido (se evita) | `<!ELEMENT nota ANY>` |
| `(a, b, c)` | Una **secuencia**: a, luego b, luego c, **en ese orden** | `(titulo, autor+, anio)` |
| `(a \| b)` | Una **elección**: a o b | `(telefono \| email)` |
| `(#PCDATA \| a \| b)*` | Contenido **mixto**: texto con etiquetas intercaladas | `<!ELEMENT parrafo (#PCDATA \| b \| i)*>` |

### Cuántas veces: los indicadores

| Indicador | Veces | En la DTD |
|---|---|---|
| (ninguno) | **exactamente una** | `titulo` |
| `?` | cero o una (opcional) | `subtitulo?` |
| `*` | cero o más | `etiqueta*` |
| `+` | una o más | `autor+` |

## Atributos: `<!ATTLIST elemento nombre tipo obligatoriedad>`

```xml
<!ATTLIST libro isbn   CDATA                    #REQUIRED
                genero (novela | ensayo | poesia) "novela">
```

| Tipo | Significa |
|---|---|
| `CDATA` | Texto cualquiera |
| `(a \| b \| c)` | Un valor de una **lista cerrada** |
| `ID` | Un identificador **único** en todo el documento |
| `IDREF` | Una referencia a un `ID` que existe |
| `NMTOKEN` | Una palabra sin espacios |

| Obligatoriedad | Significa |
|---|---|
| `#REQUIRED` | Obligatorio |
| `#IMPLIED` | Opcional |
| `#FIXED "x"` | Siempre vale `x` |
| `"valor"` | Opcional; si falta, se toma `valor` |

## Entidades propias

```xml
<!ENTITY editorial "Editorial Alfaguara">
```

En el documento, `&editorial;` se sustituye por el texto definido. Sirve para repetir un texto sin escribirlo cada vez.

## Qué pasa cuando no se cumple

Con la DTD de la biblioteca, cuatro cambios en el documento lo hacen **inválido**, y el validador explica por qué:

| Cambio en el documento | ¿Válido? | Mensaje del validador |
|---|---|---|
| Falta el elemento `autor` | no | `Element libro content does not follow the DTD, expecting (titulo , autor+ , anio , precio), got (titulo anio precio )` |
| `genero` con un valor no permitido | no | `Value "terror" for attribute genero of libro is not among the enumerated set` |
| Falta el atributo obligatorio `isbn` | no | `Element libro does not carry attribute isbn` |
| `autor` antes de `titulo` (orden distinto) | no | `Element libro content does not follow the DTD, expecting (titulo , autor+ , anio , precio), got (autor titulo anio precio )` |

## `ID` e `IDREF`: referencias dentro del documento

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE equipo [
  <!ELEMENT equipo (persona+)>
  <!ELEMENT persona (#PCDATA)>
  <!ATTLIST persona id ID #REQUIRED jefe IDREF #IMPLIED>
]>
<equipo>
  <persona id="p1">Ana</persona>
  <persona id="p2" jefe="p1">Luis</persona>
</equipo>
```

`jefe="p1"` apunta al `ID` de Ana. Si apunta a un identificador que no existe, no es válido:

**Con jefe="p9":**

```text
IDREF attribute jefe references an unknown ID "p9"
```

!!! warning "Límites de la DTD"
    Una DTD **no sabe de tipos**: no puede decir que `anio` sea un número ni que `precio` tenga dos decimales; todo el texto es texto. Tampoco entiende bien los espacios de nombres. Para eso se creó XML Schema ([2.3](03-xsd.md)).
