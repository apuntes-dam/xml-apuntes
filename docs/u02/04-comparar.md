# 2.4 DTD frente a XSD

| | DTD | XML Schema (XSD) |
|---|---|---|
| Sintaxis | Propia (no es XML) | **Es XML** |
| Tipos de datos | Solo texto (`CDATA`, `ID`…) | **Muchos**: números, fechas, booleanos, y tipos propios |
| Restricciones de valor | Solo listas (`a \| b`) | Rangos, patrones, longitudes, listas |
| Espacios de nombres | Mal soportados | **Soportados** |
| Reutilización | Entidades | Tipos con nombre, extensión y restricción |
| Número de veces | `? * +` | `minOccurs` / `maxOccurs` con cualquier número |
| Dónde va | Dentro del documento o archivo aparte | Archivo aparte (`.xsd`) |
| Tamaño | Pequeño y sencillo | Más largo |

!!! tip "Cuál usar"
    Para estructuras sencillas o formatos antiguos, la **DTD** basta y es más corta. Para datos con **tipos** (importes, fechas, rangos), espacios de nombres o formatos nuevos, usa **XSD**. Hoy casi todo lo nuevo se describe con XSD.

## Ejemplo de la diferencia

El mismo dato, el año de un libro:

```xml
<!ELEMENT anio (#PCDATA)>                 <!-- DTD: cualquier texto, incluso «mil novecientos» -->
```

```xml
<xs:element name="anio" type="Anio"/>     <!-- XSD: un entero entre 1450 y 2100 -->
```

Los dos validan que **existe** el elemento `anio`; solo el XSD valida que su **contenido** es un año.

## Otros lenguajes de esquema

Existen alternativas, como **RELAX NG** (más simple y legible que XSD) y **Schematron** (reglas con XPath). En el módulo se trabaja con **DTD** y **XSD**.
