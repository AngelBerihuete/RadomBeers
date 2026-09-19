# Guía del instructor — Random Beers: ¡Hola Quarto!

Seminario presencial de **60 minutos**. Esta guía es un guion cronometrado:
qué decir, qué abrir, qué pedir que hagan los asistentes y qué comprobar.

## Preparación previa (antes del seminario)

1. Comprueba `quarto check` en tu máquina.
2. Verifica que `01-documentos/`, `02-presentaciones/` y `presentacion/`
   renderizan sin errores (consulta el final de la guía).
3. Sube los materiales a GitHub y comparte el enlace con antelación para que
   los asistentes puedan descargarlos (o prepáralos en un USB).
4. Recuerda a los asistentes el requisito de traer R, RStudio y Quarto
   instalados.

## Materiales

- `presentacion/index.qmd` — tu presentación en revealjs.
- `01-documentos/01-hola-quarto.qmd` → `04-publicar.qmd` — ejemplos del bloque 1.
- `02-presentaciones/01-revealjs-basico.qmd` → `02-revealjs-avanzado.qmd` — bloque 2.
- `guia-asistentes.md` — chuleta para imprimir/repartir.
- `outline-sesion.txt` — resumen para enviar por correo.

---

## Bloque 1 — Documentos básicos (30 min)

### 0–5 min: Bienvenida y verificación

- Preséntate y presenta el seminario con la portada de `presentacion/index.qmd`.
- Pide a todos que abran **RStudio** y ejecuten la comprobación:
  - RStudio: *Tools > Terminal* y escribir `quarto check` (o probar a renderizar).
- Confirma que todos tienen abierto el proyecto y un `.qmd` funcionando.
- Objetivo del bloque: "al terminar, cada uno tendrá un documento HTML con
  código, figuras y texto" (el PDF se menciona como ampliación opcional).

### 5–10 min: 01-hola-quarto.qmd

**Qué hacer:** abre `01-documentos/01-hola-quarto.qmd` como ejemplo terminado,
pero pídeles que **no lo copien**: que creen un archivo nuevo en RStudio
(*File > New File > Quarto Document*) con formato HTML.

**Qué explicar:**
- Un `.qmd` tiene tres zonas: **YAML** (cabecera entre `---`), **texto** en
  Markdown y **chunks** de código R.
- El botón **Render** (`Ctrl+Shift+K`) genera el HTML.
- Cambiar `format: html` por `format: pdf` (ver 04) cambia el motor sin tocar
  el contenido.

**Ejercicio:** escribir el título, su nombre y un párrafo "¡Hola Quarto!".
Renderizar.

**Comprobar:** que el HTML abre en el visor de RStudio.

### 10–15 min: 02-estructura.qmd

**Qué hacer:** sobre su documento, añadir:
- Un `## Título de sección`, una lista con `-` y una lista numerada.
- Un enlace: `[Quarto](https://quarto.org)`.
- Una tabla Markdown sencilla (por ejemplo, resumen de un tema de clase).

**Qué explicar:**
- Los `#` crean títulos; en HTML generan una estructura navegable.
- Añadir opciones al YAML: `toc: true`, `theme: cosmo`, `lang: es`.
- `date: last-modified` muestra la fecha automática.

**Ejercicio:** activar `toc: true` y `theme: cosmo` y re-renderizar.

**Comprobar:** que aparece el índice a la izquierda y cambia el tema.

### 15–20 min: 03-codigo.qmd

**Qué hacer:** abrir `01-documentos/03-codigo.qmd` y, en su documento, insertar
un chunk con el botón *Insert > R* o tecleando:

    ```{r}
    summary(iris)
    ```

**Qué explicar:**
- El chunk se ejecuta al renderizar; el resultado aparece en el documento.
- Código **en línea** (inline): `` `r mean(iris$Petal.Length)` `` inserta el
  resultado dentro de una frase.
- Figuras: `hist(faithful$waiting, col = "skyblue")` genera una gráfica.

**Ejercicio:** añadir `hist` y `boxplot(Petal.Length ~ Species, data = iris)`.

**Comprobar:** que las figuras aparecen debajo de su chunk.

### 20–25 min: 04-publicar.qmd

**Qué hacer:** mostrar `01-documentos/04-publicar.qmd` (renderiza en HTML, como
todos los documentos del seminario).

**Qué explicar:**
- Se pueden definir varios formatos a la vez, pero en el seminario usamos
  **HTML** para no depender de LaTeX en los portátiles de los asistentes.
- El **PDF es una ampliación opcional**: añadir al YAML

      format:
        html: default
        pdf: default

  Requiere LaTeX. Si no está instalado, se instala con `quarto install tinytex`
  (necesita internet y puede tardar unos minutos, por eso no lo hacemos en la
  sesión).
- Matemáticas con `$...$` o `$$...$$` (útil en estadística).

**Ejercicio:** añadir una ecuación (p. ej. la media `$$\bar{x}=\frac{\sum x_i}{n}$$`) y re-renderizar.

**Comprobar:** que el HTML se regenera con la fórmula.

### 25–30 min: Repaso del bloque 1

- Repasar las opciones de chunk que ya han visto: `echo`, `fig.width`.
- Preguntar dudas y destacar la chuleta (`guia-asistentes.md`).
- Transición: "todo lo que hemos hecho en HTML vale para presentaciones:
  Quarto genera diapositivas con el mismo `.qmd`".

---

## Bloque 2 — Presentaciones revealjs (30 min)

### 30–35 min: 01-revealjs-basico.qmd

**Qué hacer:** abrir `02-presentaciones/01-revealjs-basico.qmd`. Pedir que
cambien el `format` de su último documento a `revealjs` y lo rendericen.

**Qué explicar:**
- Con `format: revealjs` cada encabezado `##` es una diapositiva.
- El YAML controla el tema (`theme: serif`), tamaño de fuente y el título.
- Navegación con las flechas del teclado o espacio; `Esc` para el índice.

**Ejercicio:** crear 3 diapositivas: portada, "objetivos" y una con una lista.

**Comprobar:** que aparece la presentación a pantalla completa.

### 35–40 min: 02-revealjs-avanzado.qmd

**Qué hacer:** abrir `02-presentaciones/02-revealjs-avanzado.qmd`.

**Qué explicar:**
- **Fragmentos**: se revela el contenido poco a poco añadiendo `.fragment`:

      ::: {.fragment}
      Aparece al pulsar la flecha
      :::

- **Dos columnas**: con `::: {.columns}` y `::: {.column width="50%"}`.
- **Figuras desde R**: un chunk `{r}` dentro de una diapositiva genera la
  gráfica en la propia diapositiva.

**Ejercicio:** convertir la diapositiva de objetivos en fragmentos y añadir un
gráfico de `iris` en una columna.

**Comprobar:** que los elementos aparecen paso a paso y el gráfico se ve.

### 40–45 min: opciones de chunks y personalización

**Qué explicar (con ejemplos rápidos):**
- `echo: false` oculta el código y muestra solo el resultado.
- `fig.width` / `fig.height` para tamaño de figuras.
- `message: false` / `warning: false` para limpiar la salida.
- En revealjs se puede fijar un **fondo de color** en una diapositiva:

      ## Título {background-color="#f7f7f7"}

**Ejercicio:** en su presentación, ocultar el código de un chunk (`echo: false`)
y cambiar el fondo de una diapositiva.

### 45–50 min: buenas prácticas para docencia

- Un mismo `.qmd` sirve para **apuntes** (html/pdf) y para **transparencias**
  (revealjs): la fuente es única.
- Reproducibilidad: si cambian los datos, el documento se regenera completo.
- Guardar figuras con `echo: false` y `fig.cap` para citarlas en los apuntes.

### 50–55 min: dudas y repaso

- Revisar juntos la chuleta (`guia-asistentes.md`) punto por punto.
- Resolver dudas individuales (es el momento de caminar entre los asistentes).

### 55–60 min: cierre

- Resumen: qué es Quarto, cómo renderizar, formatos html/pdf/revealjs.
- Recordar dónde están los materiales (repositorio GitHub).
- Pedir evaluación breve (papel o formulario) y agradecer la asistencia.

---

## Fallos típicos y soluciones

| Problema | Solución |
| --- | --- |
| `quarto` no se reconoce en la terminal | Reinstalar Quarto y reiniciar RStudio/terminal. |
| El HTML no aparece tras Render | Mirar la pestaña *Output* de RStudio; suele ser un error de YAML (comillas sin cerrar). |
| El PDF da error de LaTeX | Es una ampliación opcional; instalar TinyTeX con `quarto install tinytex` (necesita internet). |
| `hist()` no sale en la diapositiva | Asegurarse de que el chunk `{r}` está **dentro** de la diapositiva (`##`). |
| Los fragmentos no aparecen | Revisar la sintaxis `::: {.fragment}` y que está bien indentada (dos espacios). |
| El idioma de la salida está en inglés | Añadir `lang: es` al YAML. |

## Lista de verificación final (probar antes del seminario)

Todos los documentos renderizan a **HTML**, así que solo se necesita Quarto
instalado (sin LaTeX):

```bash
for f in 01-documentos/*.qmd 02-presentaciones/*.qmd presentacion/index.qmd; do
  quarto render "$f"
done
```