# Chuleta — Random Beers: ¡Hola Quarto!

Resumen rápido para tener a mano durante y después del seminario.

## 1. Estructura de un documento `.qmd`

Un archivo Quarto tiene tres zonas:

```yaml
---
title: "Título"
author: "Tu nombre"
date: last-modified
format: html            # html, pdf, docx o revealjs
toc: true               # índice en documentos
lang: es
---
```

Después del YAML va el texto en **Markdown** y los **chunks** de código R.

## 2. Markdown básico

```markdown
# Título nivel 1
## Título nivel 2
### Título nivel 3

- elemento de lista
- otro elemento

1. primero
2. segundo

[texto del enlace](https://quarto.org)

**negrita**   *cursiva*
```

Tabla:

```markdown
| Variable | Media |
|----------|-------|
| Altura   | 5.8   |
| Peso     | 70    |
```

## 3. Chunks de código R

Insertar un chunk: *Code > Insert Chunk* o teclear:

````markdown
```{r}
summary(iris)
```
````

Opciones de chunk útiles (van en la primera línea):

```markdown
{r, echo = FALSE}      # ejecuta pero no muestra el código
{r, warning = FALSE}   # oculta avisos
{r, fig.width = 6}     # ancho de la figura en pulgadas
{r, message = FALSE}   # oculta mensajes
```

Código en línea (inline) para meter resultados dentro de una frase:

```markdown
La media es `r mean(iris$Petal.Length)`.
```

## 4. Figuras (R base y ggplot2)

R base:

```r
hist(faithful$waiting, col = "skyblue", main = "Tiempos de espera")
boxplot(Petal.Length ~ Species, data = iris, col = "lightgreen")
plot(cars, pch = 19, col = "steelblue")
```

ggplot2 (con `penguins`):

```r
library(tidyverse)
library(palmerpenguins)

ggplot(penguins, aes(x = flipper_length_mm, y = body_mass_g, color = species)) +
  geom_point()
```

Matriz de correlación con `PerformanceAnalytics`:

```r
library(PerformanceAnalytics)
penguins_num <- penguins |>
  select(bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g) |>
  drop_na()
chart.Correlation(penguins_num, histogram = TRUE)
```

## 5. Formatos de salida

**HTML** es el formato por defecto y el que usamos en el seminario: no requiere
nada más que Quarto.

```yaml
format: html
```

Otros formatos (el **PDF** es opcional, necesita LaTeX):

```yaml
format:
  html: default
  pdf: default
  docx: default
```

```bash
quarto install tinytex   # instala LaTeX si no lo tienes (necesita internet)
```

`Ctrl+Shift+K` (Windows/Linux) o `Cmd+Shift+K` (macOS) para **Render**.

## 6. Plugins para docencia

### Callouts (bloques destacados)

```markdown
::: {.callout-note}
Nota.
:::

::: {.callout-tip}
Consejo.
:::

::: {.callout-warning}
Aviso.
:::

::: {.callout-important}
Importante.
:::
```

### Tabsets (pestañas)

```markdown
::: {.panel-tabset}
### Código
código…
### Resultado
resultado…
:::
```

### Referencias cruzadas

```markdown
```{r}
#| label: fig-histograma
#| fig-cap: "Histograma"
hist(faithful$waiting)
```

La @fig-histograma muestra la distribución.
```

Etiquetas: `#fig-`, `#tbl-`, `#eq-`; se citan con `@fig-`, `@tbl-`, `@eq-`.

### Imágenes

```markdown
![Logo del seminario](../logo.jpg){#fig-logo width=200px}

La @fig-logo ilustra el seminario.
```

### Referencias a secciones

Añade `number-sections: true` al YAML, etiqueta el encabezado con `{#sec-...}`
y cítalo con `@sec-...`:

```markdown
## Histograma {#sec-histograma}

Véase la @sec-histograma.
```

### Tablas con título

```markdown
```{r}
#| label: tbl-resumen
#| tbl-cap: "Media por especie"
aggregate(Sepal.Length ~ Species, data = iris, FUN = mean) |>
  knitr::kable()
```

La @tbl-resumen se cita por número.
```

### Emojis

Activa `from: markdown+emoji` en el YAML y usa *shortcodes* (`:bulb:`,
`:warning:`, `:bar_chart:`) o pega el carácter emoji directamente.

### Notas al pie

```markdown
El coeficiente de correlación^[Entre -1 y 1] mide la relación lineal.
```

### Citas bibliográficas

```yaml
bibliography: references.bib
```

Citar con `@clave`; la bibliografía se genera sola.

### webexercises (ejercicios autoevaluables)

Necesita `install.packages("webexercises")` y la configuración del proyecto
(ya incluida). En el documento, cargar el paquete en un chunk `include: false`:

```markdown
`r fitb(4)`          # rellenar un hueco
`r mcq(c("a", answer = "b", "c"))`   # tipo test
`r torf(TRUE)`       # verdadero/falso
`r hide("Solución")` ... `r unhide()`  # solución oculta
```

## 7. Presentaciones revealjs

Con `format: revealjs`, cada `##` es una diapositiva.

```yaml
---
title: "Mi presentación"
format: revealjs
theme: serif
---
```

- **Fragmento** (aparece paso a paso):

```markdown
::: {.fragment}
Texto que aparece al avanzar
:::
```

- **Dos columnas**:

```markdown
::: {.columns}
::: {.column width="50%"}
Contenido izquierda
:::
::: {.column width="50%"}
Contenido derecha
:::
:::
```

- **Fondo de color en una diapositiva**:

```markdown
## Título {background-color="#f7f7f7"}
```

- Un chunk `{r}` dentro de una diapositiva dibuja la figura ahí mismo.

### Plugins de revealjs

```yaml
format:
  revealjs:
    theme: simple
    slide-number: true
    chalkboard: true   # pizarra (tecla B)
    menu: true         # menú lateral
    zoom: true         # Alt + clic
```

- **Notas del orador** (vista con la tecla **S**):

```markdown
::: {.notes}
Nota que solo ve el presentador.
:::
```

- **Roughnotation** (anotaciones a mano alzada): añade `filters: - roughnotation`
  al YAML y marca el texto:

```markdown
[Texto clave]{.rn-fragment rn-type=circle rn-color=red}
```

  Tipos: `underline`, `box`, `circle`, `highlight`, `strike-through`,
  `crossed-off`, `bracket`.

## 8. Atajos y trucos

- `Ctrl+Shift+K` / `Cmd+Shift+K`: renderizar.
- Añadir `lang: es` para salida en español.
- En una presentación: flechas para navegar, `Esc` para el índice.
- Un solo `.qmd` puede ser apuntes (html/pdf) y transparencias (revealjs).

## 9. Recursos

- Documentación oficial: <https://quarto.org>
- Cheat sheets de Quarto: <https://quarto.org/docs/cheatsheets>
- Descargar Quarto: <https://quarto.org/docs/get-started>
- webexercises: <https://psyteachr.github.io/webexercises>