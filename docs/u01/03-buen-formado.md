# 1.3 Buen formado y errores típicos

Un documento está **bien formado** cuando cumple las reglas de escritura de XML. Es lo **mínimo** que se le pide: un analizador (el programa que lee XML) **se niega a leer** un documento mal formado y da un error, por pequeño que sea. HTML perdona un `<p>` sin cerrar; XML **no perdona nada**.

## Las reglas

1. Hay **un único elemento raíz**.
2. Todo elemento abierto **se cierra** (o se escribe vacío, `<a/>`).
3. Los elementos se **anidan bien**: el último en abrirse es el primero en cerrarse.
4. Los **valores de atributo van entre comillas** y un atributo no se repite en el mismo elemento.
5. **Mayúsculas y minúsculas** cuentan: la etiqueta de cierre es idéntica a la de apertura.
6. `<` y `&` en el texto se escriben como **entidades** (`&lt;`, `&amp;`).
7. Los nombres respetan las reglas de nombres (sin espacios, sin empezar por dígito).

## Los errores más típicos, con el mensaje real

| Documento | Qué falla | Mensaje del analizador (libxml2) |
|---|---|---|
| `<a><b></a>` | las etiquetas se cruzan: se cierra `a` sin haber cerrado `b` | `Opening and ending tag mismatch: b line 1 and a, line 1, column 11` |
| `<a><b>texto</B></a>` | `B` en mayúscula no cierra a `b` | `Opening and ending tag mismatch: b line 1 and B, line 1, column 16` |
| `<a>5 < 6</a>` | el `<` del texto se toma como el inicio de una etiqueta | `StartTag: invalid element name, line 1, column 7` |
| `<a x=1/>` | el valor del atributo no lleva comillas | `AttValue: " or ' expected, line 1, column 6` |
| `<a x="1" x="2"/>` | el atributo `x` está repetido | `Attribute x redefined, line 1, column 15` |
| `<a/><b/>` | hay dos elementos raíz | `Extra content at the end of the document, line 1, column 5` |
| `<a>&nbsp;</a>` | la entidad `&nbsp;` no existe en XML | `Entity 'nbsp' not defined, line 1, column 10` |
| `<a></a>
<?xml version="1.0"?>` | el prólogo no está al principio | `XML declaration allowed only at the start of the document, line 2, column 6` |

!!! tip "Cómo leer un error"
    El mensaje da la **línea** y la **columna** donde el analizador **se dio cuenta**, que suele ser un poco después de la causa. Si dice «tag mismatch», busca una etiqueta sin cerrar o mal escrita **antes** de esa posición. Si dice «Extra content at the end of the document», hay un segundo elemento raíz o texto suelto tras el primero.

## Bien formado no es válido

Que un documento esté bien formado no dice que **tenga sentido**: `<libro><precio>muy caro</precio></libro>` está bien formado, aunque el precio no sea un número. Para comprobar que respeta una estructura concreta existe la **validación** (unidad 2).
