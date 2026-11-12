# XML

Apuntes de **XML**, el lenguaje de marcas con el que se describen datos y documentos: cómo se escribe, cómo se valida, cómo se consulta y cómo se transforma. Con la misma estructura que las demás webs: teoría con **ejemplos comprobados con analizadores reales** y ejercicios con soluciones.

!!! info "Cómo está organizado"
    Tres unidades: **escribir** documentos XML, **validarlos** (DTD y XSD) y **consultar y transformar** (XPath y XSLT), con una última página sobre cómo leerlos desde un programa.

| Apartado | Contenido |
|---|---|
| [U1. Documentos XML](u01/index.md) | Qué es XML, estructura, buen formado, espacios de nombres y herramientas |
| [U2. Validación](u02/index.md) | Bien formado y válido, DTD y XML Schema (XSD) |
| [U3. Consultar y transformar](u03/index.md) | XPath, XSLT y XML desde Python, Java y C# |
| [Prácticas](u01/practicas.md) | Guía de prácticas |

!!! note "Qué es XML"
    XML es un **metalenguaje**: no tiene etiquetas propias, sino reglas para crear lenguajes de marcas. De él nacen SVG (gráficos), MathML (fórmulas), GML (mapas), RSS (noticias), XHTML, XSLT y XSD, y se usa en configuración (Android, Maven, .NET) y en documentos (Office).

!!! warning "XML y programación"
    XML no es un lenguaje de programación: aquí no hay «programas» que ejecutar, sino **documentos que se comprueban**. Los ejercicios son de escribir XML, esquemas, consultas y hojas de estilo, y cada solución se ha comprobado con un analizador real.
