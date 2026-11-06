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
2. Instala los paquetes de R usados en el seminario:

   ```r
   install.packages(c("tidyverse", "palmerpenguins",
                      "PerformanceAnalytics", "webexercises"))
   ```

3. Verifica que todos los `.qmd` renderizan (consulta la lista al final).
4. Sube los materiales a GitHub y comparte el enlace antes de la primera sesión.
5. Recuerda a los asistentes instalar R, RStudio, Quarto y esos paquetes.

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

### 40–55 min: Elementos importantes — `04-elementos-importantes.qmd`

**Qué hacer:** abrir `04-elementos-importantes.qmd`, que ya carga `tidyverse`,
`palmerpenguins` y `PerformanceAnalytics`.

**Qué explicar:** el chunk se ejecuta al renderizar; el código en línea
inserta resultados dentro de una frase; los gráficos se generan con `ggplot2`
sobre los datos `penguins`; y `chart.Correlation()` de `PerformanceAnalytics`
muestra la matriz de correlación. Además se ven las **referencias cruzadas** a
figuras (`fig-cap` + `#fig-`), imágenes, tablas (`#tbl-`), ecuaciones (`#eq-`) y
secciones (`#sec-` + `number-sections: true`), junto con citas bibliográficas y
notas al pie.

**Ejercicio:** añadir un gráfico de dispersión (`geom_point`), calcular con
código en línea la media de `body_mass_g` y etiquetar una ecuación para citarla.

**Comprobar:** que las figuras aparecen debajo de su chunk, la matriz de
correlación se ve completa y los números de figura/tabla/ecuación se generan.

### 55–70 min: Plugins para apuntes — `05-plugins-docencia.qmd` y `06-webexercises.qmd`

**Qué hacer:** abrir `05-plugins-docencia.qmd` y `06-webexercises.qmd` ya
montados (la configuración de `webexercises` está en `_quarto.yml` e `include/`).

**Qué explicar:**
- **Callouts:** `::: {.callout-note/tip/warning/important}`.
- **Callouts colapsables:** `collapse="true"` para ocultar pistas/soluciones.
- **Tabsets:** `::: {.panel-tabset}` para código/resultado.
- **Emojis:** `from: markdown+emoji` y *shortcodes* (`:bulb:`).
- **Teoremas/definiciones:** `#def-`, `#thm-`, `::: {.proof}`.
- **Code annotation:** `# <1>` + lista numerada para explicar el código.
- **Diagramas Mermaid:** chunk `{mermaid}`.
- **webexercises:** `fitb()`, `mcq()`, `torf()`, `hide()/unhide()`.

**Ejercicio:** añadir a su documento un callout de consejo y una definición
numerada.

**Comprobar:** que los callouts y las definiciones/teoremas se numeran bien.

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

Dinámica: los asistentes reciben los `.qmd` de `02-sesion-presentaciones/`, los
modifican siguiendo cada bloque ("cambia esto, renderiza y observa") y pueden
volver al original si algo se rompe. El orden coincide con la presentación
`sesion2-presentaciones.qmd`.

### 0–8 min: Repaso y verificación

- Recapitula la sesión 1 (formato Quarto, chunks, render).
- Objetivo: "al terminar, cada uno tendrá una presentación revealjs con
  fragmentos, figuras de R y notas del orador".
- Pide que abran `01-revealjs-basico.qmd` y comprueben que renderiza.

### 8–23 min: Primeras diapositivas — `01-revealjs-basico.qmd`

**Qué explicar:** con `format: revealjs` cada `##` es una diapositiva; el YAML
controla el tema; navegación con flechas, `Esc` para el índice y **F** para
pantalla completa.

**Ejercicio:** cambiar el `theme` y añadir una diapositiva con una lista.

**Comprobar:** que cambia el tema y la nueva diapositiva se ve bien.

### 23–35 min: R en las diapositivas — `02-r-diapositivas.qmd`

**Qué explicar:** los chunks `{r}` se ejecutan al renderizar; el código en línea
inserta resultados; `echo: false` muestra solo la figura.

**Ejercicio:** cambiar la variable del gráfico, probar `echo: false` y añadir un
resultado en línea.

**Comprobar:** que la diapositiva queda limpia (solo figura/resultado).

### 35–52 min: Maquetación y estilos — `03-maquetacion.qmd` y `03-maquetacion-css.qmd`

**Qué explicar:** **fragmentos** (`::: {.fragment}`), contrastados con listas
`{.incremental}` (envuelven toda la lista), y **columnas**
(`::: {.columns}` / `::: {.column width="50%"}`); `transition` /
`background-transition`; fondos de color con `{background-color="#..."}` y color de texto con
`style=`. Después, `03-maquetacion-css.qmd`: la hoja
`estilos-personalizados.css` se enlaza con `css:` en el YAML y contiene un
fondo degradado y un bloque personalizado.

**Ejercicio:** convertir la diapositiva de objetivos en fragmentos, cambiar la
`transition` y el color de fondo de una diapositiva; en la versión CSS, cambiar
los colores del degradado y volver a renderizar.

**Comprobar:** que los elementos aparecen paso a paso y que el cambio en el CSS
se refleja tras renderizar.

### 52–67 min: Plugins de revealjs — `04-plugins-revealjs.qmd`

**Qué explicar:** `controls` (flechas laterales), `chalkboard` (pizarra, tecla
**B**), `menu` (menú lateral), `zoom` (**Alt** + clic), `slide-number`;
**notas del orador** con `::: {.notes}` y vista del presentador (**S**);
**roughnotation** (`filters: - roughnotation` y
`[texto]{.rn-fragment rn-type=circle rn-color=red}`); `embed-resources: true`
(un único HTML autocontenido, útil para proyectar sin conexión, pero
incompatible con `chalkboard`); exportar a PDF abriendo el HTML con
`?print-pdf` en la URL e imprimiendo desde el navegador.

**Ejercicio:** poner `controls: false` y volver a `true`, probar la pizarra
(tecla **B**), añadir una nota del orador y marcar una palabra con
roughnotation.

**Comprobar:** que las flechas, la pizarra, las notas y la anotación
funcionan.

### 67–87 min: Ejercicio (20 min)

**Ejercicio:** construir una presentación de un tema de estadística:
1. Crear un `.qmd` con `format: revealjs`.
2. Añadir portada, objetivos (fragmentos) y un gráfico de R.
3. Añadir notas del orador y activar `chalkboard`.
4. Opcional: aplicar un CSS propio y marcar una idea con roughnotation.
5. Comparar con `ejercicio/presentacion-tema.qmd`.

### 87–90 min: Cierre

Puesta en común, recordar la chuleta (`guia-asistentes.md`) y los materiales
del repositorio.

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
| Error "not compatible with self-contained output" | `embed-resources: true` no admite `chalkboard`; desactiva uno de los dos. |
| El idioma de la salida está en inglés | Añadir `lang: es` al YAML. |

## Lista de verificación final (antes de cada sesión)

```bash
for f in 01-sesion-documentos/*.qmd 01-sesion-documentos/ejercicio/*.qmd \
         02-sesion-presentaciones/*.qmd 02-sesion-presentaciones/ejercicio/*.qmd \
         presentacion/*.qmd; do
  quarto render "$f"
done
```