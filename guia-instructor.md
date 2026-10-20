# Guía del instructor — Random Beers: ¡Hola Quarto!

Seminario presencial en **dos sesiones de 90 minutos**. Esta guía es un guion
cronometrado: qué decir, qué abrir, qué pedir que hagan los asistentes y qué
comprobar.

## Datos del seminario

- **Lugar:** Sala de reuniones del Departamento de Estadística e Investigación
  Operativa.
- **Sesión 1:** viernes 30 de octubre, 12:00–13:30. Imparte Ángel, ayuda Raúl.
- **Sesión 2:** viernes 6 de noviembre, 12:00–13:30. Imparte Raúl, ayuda Ángel.
- **Contacto:** angel.berihuete@uca.es

## Preparación previa

1. Comprueba `quarto check` en tu máquina.
2. Instala el paquete `webexercises` (necesario para la sesión 1):
   `install.packages("webexercises")`.
3. Verifica que todos los `.qmd` renderizan (consulta la lista al final).
4. Sube los materiales a GitHub y comparte el enlace antes de la primera sesión.
5. Recuerda a los asistentes instalar R, RStudio, Quarto y `webexercises`.

## Materiales

- `presentacion/sesion1-documentos.qmd` y `sesion2-presentaciones.qmd` — las
  presentaciones del ponente.
- `01-sesion-documentos/` — documentos progresivos de la sesión 1.
- `02-sesion-presentaciones/` — presentaciones progresivas de la sesión 2.
- `guia-asistentes.md` — chuleta para repartir.
- `outline-sesion.txt` — resumen para enviar por correo.

---

# Sesión 1 — Generación de apuntes y prácticas (90 min)

### 0–10 min: Bienvenida y verificación

- Preséntate y presenta la sesión con la portada de `sesion1-documentos.qmd`.
- Pide a todos que abran **RStudio** y comprueben la instalación:
  `quarto check` en la terminal.
- Objetivo: "al terminar, cada uno tendrá un documento HTML con código, figuras
  y ejercicios interactivos".

### 10–25 min: El formato Quarto — `01-hola-quarto.qmd`

**Qué hacer:** muestra `01-hola-quarto.qmd` como ejemplo terminado, pero pídeles
que **no lo copien**: que creen un archivo nuevo (*File > New File > Quarto
Document*) con formato HTML.

**Qué explicar:** las tres zonas del `.qmd` (YAML, Markdown, chunks) y el botón
**Render** (`Ctrl+Shift+K`).

**Ejercicio:** escribir título, autor y un párrafo "¡Hola Quarto!" y renderizar.

**Comprobar:** que el HTML abre en el visor.

### 25–40 min: Compilación y formatos — `02-estructura.qmd` y `03-formatos-salida.qmd`

**Qué hacer:** sobre su documento, añadir `##` secciones, listas, enlaces y una
tabla; luego activar `toc: true` y `theme: cosmo` en el YAML.

**Qué explicar:** `format: html` es el formato por defecto (sin dependencias).
Los formatos `pdf` y `docx` se añaden al YAML; el PDF es opcional (LaTeX). La
compilación es siempre el botón **Render**.

**Ejercicio:** activar `toc: true`, re-renderizar, y añadir una fórmula con
`$$...$$` (la media).

**Comprobar:** que aparece el índice y la fórmula.

### 40–55 min: Código R — `04-codigo-r.qmd`

**Qué hacer:** insertar un chunk con el botón *Insert > R* o tecleando
```` ```{r} ```` y `summary(iris)`.

**Qué explicar:** el chunk se ejecuta al renderizar; el código en línea
`` `r mean(...)` `` inserta resultados dentro de una frase; las figuras
(`hist`, `boxplot`, `plot`) se generan automáticamente.

**Ejercicio:** añadir `hist(faithful$waiting)` y
`boxplot(Petal.Length ~ Species, data = iris)`.

**Comprobar:** que las figuras aparecen debajo de su chunk.

### 55–70 min: Plugins para docencia — `05-plugins-docencia.qmd` y `06-webexercises.qmd`

**Qué hacer:** abrir `05-plugins-docencia.qmd` y `06-webexercises.qmd` ya
montados (la configuración de `webexercises` está en `_quarto.yml` e `include/`).

**Qué explicar:**
- **Callouts:** `::: {.callout-note/tip/warning/important}`.
- **Tabsets:** `::: {.panel-tabset}` para código/resultado.
- **Referencias cruzadas:** `#fig-`, `#tbl-`, `#eq-` y citarlas con `@fig-...`.
- **Citas:** `bibliography: referencias.bib` y `@clave`.
- **webexercises:** `fitb()`, `mcq()`, `torf()`, `hide()/unhide()`.

**Ejercicio:** añadir a su documento un callout de consejo y una referencia
cruzada a su figura.

**Comprobar:** que los callouts y los números de figura se generan bien.

### 70–90 min: Ejercicio (20 min) — de beamer a Quarto

**Qué hacer:** plantear el ejercicio: pasar `ejercicio/apuntes-beamer.tex` a un
documento Quarto. Los asistentes trabajan 20 minutos; Raúl (apoyo) resuelve
dudas individuales.

**Pasos del ejercicio:**
1. Abrir `apuntes-beamer.tex` y leer el contenido.
2. Crear un `.qmd` con las fórmulas, listas y el histograma.
3. Sustituir la figura "de relleno" por un chunk `{r}` con `hist()`.
4. Calcular media/varianza con código en línea.
5. Comparar con la solución `apuntes-quarto.qmd`.

**Cierre:** puesta en común de dudas y recordatorio de la sesión 2.

---

# Sesión 2 — Generación de presentaciones (90 min)

### 0–10 min: Repaso y verificación

- Recapitula la sesión 1 (formato Quarto, chunks, render).
- Objetivo: "al terminar, cada uno tendrá una presentación revealjs con
  fragmentos, figuras de R y notas del orador".

### 10–25 min: Primeras diapositivas — `01-revealjs-basico.qmd`

**Qué hacer:** abrir `01-revealjs-basico.qmd` y pedir que cambien el `format`
de su documento a `revealjs` y lo rendericen.

**Qué explicar:** con `format: revealjs` cada `##` es una diapositiva; el YAML
controla el tema; navegación con flechas y `Esc` para el índice.

**Ejercicio:** crear portada, "objetivos" y una diapositiva con una lista.

**Comprobar:** que aparece la presentación a pantalla completa.

### 25–40 min: Maquetación — `02-maquetacion.qmd`

**Qué hacer:** abrir `02-maquetacion.qmd`.

**Qué explicar:** **fragmentos** (`::: {.fragment}`) y **columnas**
(`::: {.columns}` / `::: {.column width="50%"}`); fondos de color con
`{background-color="#..."}`.

**Ejercicio:** convertir la diapositiva de objetivos en fragmentos y añadir un
gráfico de `iris` en una columna.

**Comprobar:** que los elementos aparecen paso a paso.

### 40–55 min: R en las diapositivas — `03-r-diapositivas.qmd`

**Qué hacer:** abrir `03-r-diapositivas.qmd`.

**Qué explicar:** los chunks `{r}` se ejecutan al renderizar; el código en línea
inserta resultados; `echo: false` muestra solo la figura.

**Ejercicio:** añadir una figura con `echo: false` y un resultado en línea.

**Comprobar:** que la diapositiva queda limpia (solo figura/resultado).

### 55–70 min: Plugins de revealjs — `04-plugins-revealjs.qmd`

**Qué hacer:** abrir `04-plugins-revealjs.qmd`.

**Qué explicar:** `chalkboard` (pizarra, tecla **B**), `menu` (menú lateral),
`zoom` (**Alt** + clic), `slide-number`; **notas del orador** con `::: {.notes}`
y vista del presentador (**S**); personalización con `theme` y `css`.

**Ejercicio:** activar `chalkboard` y añadir una nota del orador.

**Comprobar:** que la pizarra y las notas funcionan.

### 70–90 min: Ejercicio + cierre

**Ejercicio:** construir una presentación de un tema de estadística:
1. Crear un `.qmd` con `format: revealjs`.
2. Añadir portada, objetivos (fragmentos) y un gráfico de R.
3. Añadir notas del orador y activar `chalkboard`.
4. Comparar con `ejercicio/presentacion-tema.qmd`.

**Cierre:** puesta en común, recordar la chuleta (`guia-asistentes.md`) y los
materiales del repositorio.

---

## Fallos típicos y soluciones

| Problema | Solución |
| --- | --- |
| `quarto` no se reconoce | Reinstalar Quarto y reiniciar RStudio/terminal. |
| El HTML no aparece tras Render | Mirar *Output*; suele ser un error de YAML (comillas sin cerrar). |
| `webexercises` no funciona | Comprobar `install.packages("webexercises")` y re-renderizar. |
| El PDF da error de LaTeX | Es opcional; `quarto install tinytex` (necesita internet). |
| Los fragmentos no aparecen | Revisar `::: {.fragment}` con indentación de dos espacios. |
| La pizarra no se abre | Verificar `chalkboard: true` en el YAML y re-renderizar. |
| El idioma de la salida está en inglés | Añadir `lang: es` al YAML. |

## Lista de verificación final (antes de cada sesión)

```bash
for f in 01-sesion-documentos/*.qmd 01-sesion-documentos/ejercicio/*.qmd \
         02-sesion-presentaciones/*.qmd 02-sesion-presentaciones/ejercicio/*.qmd \
         presentacion/*.qmd; do
  quarto render "$f"
done
```