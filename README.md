# Random Beers — ¡Hola Quarto

Seminario presencial de 60 minutos para profesorado de estadística sobre cómo
crear documentos y presentaciones con **Quarto** desde **RStudio**.

## Contenido del seminario

- **Bloque 1 (30 min):** documentos básicos en Quarto (`.qmd`).
- **Bloque 2 (30 min):** presentaciones básicas en **revealjs**.

Los materiales son documentos progresivos: cada archivo parte del anterior y
añade un concepto nuevo. Los asistentes trabajan continuamente mientras el
ponente introduce los conceptos.

## Requisitos previos

Cada asistente debe llevar un portátil con:

1. **R** (>= 4.0) — <https://cran.r-project.org>
2. **RStudio** (>= 2023.09) — <https://posit.co/download/rstudio-desktop>
3. **Quarto** (>= 1.4) — <https://quarto.org/docs/get-started>
   - En RStudio se puede comprobar en _Tools > Check for Updates_ o instalarlo
     desde <https://quarto.org/docs/download>
4. **Conexión a internet** (para descargar paquetes la primera vez).

### Verificación rápida

```bash
quarto check
```

Debe responder algo como `[✓] Your system should be ready for Quarto!`.

### Paquetes de R

Los documentos usan **R base** (no hace falta `tidyverse`). Solo se recomienda
tener instalado `rmarkdown`, que normalmente viene con RStudio:

```r
install.packages("rmarkdown")
```

## Estructura del repositorio

```
README.md                  → este archivo
outline-sesion.txt         → resumen de la sesión (para enviar por correo)
logo.jpg                   → logo del seminario
guia-instructor.md/.pdf    → guion cronometrado para el ponente
guia-asistentes.md/.pdf    → chuleta para los asistentes
presentacion/index.qmd     → presentación revealjs del seminario
01-documentos/             → bloque 1 (documentos), de menor a mayor complejidad
02-presentaciones/         → bloque 2 (revealjs), de menor a mayor complejidad
```

## Cómo usar los materiales

1. Abre el proyecto en RStudio: _File > Open Project_.
2. Abre cada `.qmd` y pulsa **Render** (atajo `Ctrl+Shift+K` en Windows/Linux,
   `Cmd+Shift+K` en macOS).
3. Los archivos de `01-documentos/` renderizan a **HTML**. Los de
   `02-presentaciones/` y `presentacion/` renderizan a **revealjs**.

> **Sobre el formato PDF:** durante el seminario se usa **HTML** para no
> depender de la instalación de LaTeX en cada portátil. La salida a **PDF** es
> opcional: se explica en `04-publicar.qmd` como ampliación y solo requiere
> añadir `pdf: default` al YAML y tener TinyTeX (`quarto install tinytex`).

## Generar los PDF de las guías

Las guías (`guia-instructor.md`, `guia-asistentes.md`) también se entregan en
PDF. Para regenerarlos:

```bash
quarto render guia-instructor.md --to pdf
quarto render guia-asistentes.md --to pdf
```

## Publicar en GitHub

```bash
git init
git add .
git commit -m "Random Beers: materiales del seminario ¡Hola Quarto!"
# Crear el repositorio (si gh está configurado)
gh repo create randombeers --public --source=. --push
```
