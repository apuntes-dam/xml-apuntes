# 2.3 XML Schema (XSD)

**XML Schema** (archivo `.xsd`) describe la estructura de un documento **escribiéndola en XML**, con **tipos de datos** (números, fechas, textos con patrón…) y soporte de espacios de nombres. Es el sustituto moderno de la DTD.

## El esquema de la biblioteca

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="biblioteca">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="libro" type="Libro" maxOccurs="unbounded"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

  <xs:complexType name="Libro">
    <xs:sequence>
      <xs:element name="titulo" type="xs:string"/>
      <xs:element name="autor"  type="xs:string" maxOccurs="unbounded"/>
      <xs:element name="anio"   type="Anio"/>
      <xs:element name="precio" type="Precio"/>
    </xs:sequence>
    <xs:attribute name="isbn"   type="Isbn" use="required"/>
    <xs:attribute name="genero" type="Genero" default="novela"/>
  </xs:complexType>

  <xs:simpleType name="Isbn">
    <xs:restriction base="xs:string">
      <xs:pattern value="978-\d{2}-\d{3,4}-\d{3,4}-\d"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="Genero">
    <xs:restriction base="xs:string">
      <xs:enumeration value="novela"/>
      <xs:enumeration value="ensayo"/>
      <xs:enumeration value="poesia"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="Anio">
    <xs:restriction base="xs:integer">
      <xs:minInclusive value="1450"/>
      <xs:maxInclusive value="2100"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:complexType name="Precio">
    <xs:simpleContent>
      <xs:extension base="xs:decimal">
        <xs:attribute name="moneda" type="xs:string" use="required"/>
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>

</xs:schema>
```

Con este esquema, la biblioteca de ejemplo es **válida**. Se enlaza desde el documento con un atributo, o se pasa al validador directamente:

```xml
<biblioteca xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:noNamespaceSchemaLocation="biblioteca.xsd">
```

## Las piezas

| Pieza | Para qué |
|---|---|
| `xs:schema` | Raíz del esquema; declara el prefijo `xs` del espacio de nombres de XML Schema |
| `xs:element` | Declara un elemento: `name`, `type`, `minOccurs`, `maxOccurs` |
| `xs:attribute` | Declara un atributo: `use="required"` (obligatorio) o `optional`, y `default` o `fixed` |
| `xs:complexType` | Un tipo con **hijos o atributos** |
| `xs:simpleType` | Un tipo **de solo texto**, normalmente una restricción de otro |
| `xs:sequence` / `xs:choice` / `xs:all` | Los hijos van **en orden** / **uno de ellos** / **en cualquier orden** |
| `xs:restriction` | Limita un tipo base: `enumeration`, `pattern`, `minInclusive`, `maxLength`… |

### Veces que aparece un elemento

`minOccurs` y `maxOccurs` (por defecto, 1 y 1):

| En el XSD | Equivale en DTD |
|---|---|
| `minOccurs="0"` (y `maxOccurs="1"`) | `?` |
| `minOccurs="0" maxOccurs="unbounded"` | `*` |
| `minOccurs="1" maxOccurs="unbounded"` | `+` |

### Tipos de datos predefinidos más usados

`xs:string`, `xs:integer`, `xs:decimal`, `xs:boolean`, `xs:date` (`2026-11-12`), `xs:dateTime`, `xs:positiveInteger`, `xs:anyURI`.

### Tipos propios por restricción

```xml
<xs:simpleType name="Anio">
  <xs:restriction base="xs:integer">
    <xs:minInclusive value="1450"/>
    <xs:maxInclusive value="2100"/>
  </xs:restriction>
</xs:simpleType>
```

Crea un tipo `Anio`: un entero entre 1450 y 2100. Un `pattern` usa una expresión regular (`978-\d{2}-…`) y una `enumeration` lista los valores permitidos.

## Lo que detecta un validador XSD

Partiendo de la biblioteca válida, estos cambios la hacen inválida; el mensaje sale del validador real:

| Cambio en el documento | Mensaje del validador (XSD) |
|---|---|
| El año no es un número | `Element 'anio': 'mil novecientos' is not a valid value of the atomic type 'Anio'.` |
| El año está fuera del rango (1450 a 2100) | `Element 'anio': [facet 'minInclusive'] The value '1200' is less than the minimum value allowed ('1450').` |
| El `isbn` no sigue el patrón | `Element 'libro', attribute 'isbn': [facet 'pattern'] The value '123' is not accepted by the pattern '978-\d{2}-\d{3,4}-\d{3,4}-\d'.` |
| El `genero` no es de la lista | `Element 'libro', attribute 'genero': [facet 'enumeration'] The value 'terror' is not an element of the set {'novela', 'ensayo', 'poesia'}.` |
| Falta el `precio` de un libro | `Element 'libro': Missing child element(s). Expected is ( precio ).` |
| El precio no es un decimal | `Element 'precio': 'barato' is not a valid value of the atomic type 'xs:decimal'.` |
Observa que la DTD **no podía** detectar los errores de tipo (año, precio) ni de patrón: todo era texto.
