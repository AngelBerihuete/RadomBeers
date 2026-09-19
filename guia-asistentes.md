# Chuleta — Random Beers: ¡Hola Quarto!

Resumen rápido para tener a mano durante y después del seminario.

## 1. Estructura de un documento `.qmd`

Un archivo Quarto tiene tres zonas:

```yaml
---
title: "Título"
author: "Tu nombre"
date: last-modified
format: html            # html, pdf o revealjs
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

## 4. Figuras (R base)

```r
hist(faithful$waiting, col = "skyblue", main = "Tiempos de espera")
boxplot(Petal.Length ~ Species, data = iris, col = "lightgreen")
plot(cars, pch = 19, col = "steelblue")
```

## 5. Formatos de salida

**HTML** es el formato por defecto y el que usamos en el seminario: no requiere
nada más que Quarto.

```yaml
format: html
```

El **PDF es opcional** (necesita LaTeX). Para probarlo en casa:

```yaml
format:
  html: default
  pdf: default
```

```bash
quarto install tinytex   # instala LaTeX si no lo tienes (necesita internet)
```

`Ctrl+Shift+K` (Windows/Linux) o `Cmd+Shift+K` (macOS) para **Render**.

## 6. Presentaciones revealjs

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

## 7. Atajos y trucos

- `Ctrl+Shift+K` / `Cmd+Shift+K`: renderizar.
- Añadir `lang: es` para salida en español.
- En una presentación: flechas para navegar, `Esc` para el índice.
- Un solo `.qmd` puede ser apuntes (html/pdf) y transparencias (revealjs).

## 8. Recursos

- Documentación oficial: <https://quarto.org>
- Cheat sheets de Quarto: <https://quarto.org/docs/cheatsheets>
- Descargar Quarto: <https://quarto.org/docs/get-started>