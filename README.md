# Random Beers — ¡Hola Quarto!

Seminario presencial para profesorado de estadística sobre cómo crear
documentos y presentaciones con **Quarto** desde **RStudio**.

## Sesiones

| Sesión | Fecha | Hora | Tema | Imparte | Ayuda |
| --- | --- | --- | --- | --- | --- |
| 1 | Viernes 30 de octubre | 12:00–13:30 | Generación de apuntes y prácticas | Ángel Berihuete | Raúl Páez |
| 2 | Viernes 6 de noviembre | 12:00–13:30 | Generación de presentaciones (revealjs) | Raúl Páez | Ángel Berihuete |

**Lugar:** Sala de reuniones del Departamento de Estadística e Investigación
Operativa.

Los materiales son documentos progresivos: cada archivo parte del anterior y
añade un concepto nuevo. Los asistentes trabajan continuamente mientras el
ponente introduce los conceptos.

## Requisitos previos

Cada asistente debe llevar un portátil con:

1. **R** (>= 4.0) — <https://cran.r-project.org>
2. **RStudio** (>= 2023.09) — <https://posit.co/download/rstudio-desktop>
3. **Quarto** (>= 1.4) — <https://quarto.org/docs/get-started>
4. **Conexión a internet** (para descargar paquetes la primera vez).

### Verificación rápida

```bash
quarto check
```

Debe responder algo como `[✓] Your system should be ready for Quarto!`.

### Paquetes de R

Los documentos usan **R base** y **tidyverse/ggplot2**. Instala los paquetes
necesarios para el seminario:

```r
install.packages(c("tidyverse", "palmerpenguins",
                   "PerformanceAnalytics", "webexercises"))
```

## Estructura del repositorio

```
README.md                        → este archivo
outline-sesion.txt               → resumen de las sesiones (para enviar por correo)
logo.jpg                         → logo del seminario
guia-instructor.md/.pdf          → guion cronometrado para los ponentes
guia-asistentes.md/.pdf          → chuleta para los asistentes
references.bib                   → bibliografía de ejemplo
include/                         → ficheros css/js de webexercises
_extensions/                     → extensión roughnotation (revealjs)
presentacion/                    → presentaciones revealjs del seminario
   sesion1-documentos.qmd        →   sesión 1 (Ángel)
   sesion2-presentaciones.qmd    →   sesión 2 (Raúl)
01-sesion-documentos/            → sesión 1 (documentos), de menor a mayor complejidad
   ejercicio/                    →   apuntes-beamer.tex (ejercicio) + apuntes-quarto.qmd (solución)
02-sesion-presentaciones/        → sesión 2 (revealjs), de menor a mayor complejidad
   ejercicio/                    →   presentacion-tema.qmd
```

## Cómo usar los materiales

1. Abre el proyecto en RStudio: _File > Open Project_.
2. Abre cada `.qmd` y pulsa **Render** (atajo `Ctrl+Shift+K` en Windows/Linux,
   `Cmd+Shift+K` en macOS).
3. Los archivos de `01-sesion-documentos/` renderizan a **HTML**. Los de
   `02-sesion-presentaciones/` y `presentacion/` renderizan a **revealjs**.

> **Sobre el formato PDF:** durante el seminario se usa **HTML** para no
> depender de la instalación de LaTeX en cada portátil. La salida a **PDF** es
> opcional: se explica en `03-formatos-salida.qmd` como ampliación y solo
> requiere añadir `pdf: default` al YAML y tener TinyTeX (`quarto install tinytex`).

## Generar los PDF de las guías

Las guías (`guia-instructor.md`, `guia-asistentes.md`) también se entregan en
PDF. Para regenerarlos:

```bash
quarto pandoc guia-instructor.md -o guia-instructor.pdf
quarto pandoc guia-asistentes.md -o guia-asistentes.pdf
```

## Publicar en GitHub

```bash
git init
git add .
git commit -m "Random Beers: materiales del seminario ¡Hola Quarto!"
gh repo create randombeers --public --source=. --push
```

## Autoría

Materiales preparados para el seminario **Random Beers**. Ponentes: Ángel
Berihuete y Raúl Páez. Contacto: angel.berihuete@uca.es.