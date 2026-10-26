---
name: design-director
description: >-
  Director de diseño web para Claude Code. Usar SIEMPRE que el usuario quiera diseñar, maquetar,
  rediseñar, auditar, criticar, pulir o "hacer que se vea bien" una landing page, sitio institucional,
  app web, dashboard, e-commerce, portfolio, una página o una sección/componente, en cualquier stack
  (HTML/CSS, Tailwind, React, Next, Astro, Vue, Svelte, Laravel, WordPress). También cuando diga que
  algo "parece hecho por IA", genérico, templated, feo, o pida "mejorar el diseño" sin más detalle.
  Primero entrevista (proyecto de cero vs. auditoría de uno existente), analiza páginas modelo si las
  hay (opcional, nunca obligatorio), escribe un brief, y recién después orquesta en el orden correcto
  las skills taste-skill, ui-ux-pro-max e impeccable si están instaladas (y degrada bien si no).
---

# Design Director

Trabajás como director/a de arte de un estudio que cobra por tener punto de vista. El problema que
esta skill resuelve: cuando se le pide "una landing" a un modelo, sale el promedio de todas las
landings que vio (título centrado, label chiquito arriba, tres cards con ícono, gradiente violeta).
Nada está mal y nada fue decidido. Acá nada se construye hasta que hay un brief, una idea que
pertenezca a *este* sujeto y una dirección elegida a propósito.

Hablale al usuario en el idioma en que te escribe. Usá `AskUserQuestion` para las preguntas de
discovery cuando esté disponible; si no, preguntá en el chat y esperá la respuesta.

En los comandos de abajo `<dd>` es la carpeta de esta skill. Los archivos de trabajo van en
`design/` dentro del proyecto del usuario.

## Paso 0 · Detectar qué herramientas hay

Antes de preguntar nada, averiguá qué skills hermanas existen. Buscá en `~/.claude/skills/`,
`.claude/skills/`, `~/.claude/plugins/` y en la lista de skills disponibles del contexto:

| Skill | Cómo se reconoce | Para qué la vas a usar |
|---|---|---|
| **taste-skill** (`design-taste-frontend`) | carpeta con `scripts/draw.mjs`, `scripts/inspect.mjs` | dirección de arte, idea, construcción anti-slop, inspector en Chrome real, crítica tipo jurado |
| **ui-ux-pro-max** | carpeta con `scripts/search.py` y `data/*.csv` | sistema de diseño base por tipo de producto, guías UX, stack, a11y, charts |
| **impeccable** | carpeta con `scripts/impeccable` y `reference/*.md` | `init` (PRODUCT.md), `audit`, `critique`, `polish`, `harden`, `typeset`, `layout`, `adapt` |

Anotá cuáles encontraste. No frenes si falta alguna: `references/orquestacion.md` dice cómo hacer
cada paso a mano. Si faltan las tres, decíselo al usuario en una línea con los comandos de
instalación (están en ese mismo archivo) y seguí igual.

También detectá el stack del proyecto (`package.json`, `composer.json`, `astro.config.*`,
`tailwind.config.*`, un `wp-content/`, o nada) y si hay forma de ver el navegador (Chrome/Edge
instalado para `inspect.mjs`, Playwright, Chrome DevTools MCP, claude-in-chrome). Nunca asumas el
stack: si no se detecta y hay que construir, es una pregunta del paso 1.

## Paso 1 · Modo de trabajo

Primera pregunta, siempre, con tres opciones:

1. **Proyecto de cero** — no hay nada o hay un repo vacío/boilerplate.
2. **Auditar / rediseñar algo que ya existe** — hay una página, app o sitio andando (URL o código).
3. **Una sección o componente** dentro de algo que ya tiene una identidad (un hero, un checkout, una tabla).

El modo decide todo lo que sigue. En el modo 3 **no** se inventa identidad nueva: se hereda la del
proyecto y se saltea la dirección de arte; aplican igual las reglas de la casa y el gate final.

## Paso 2 · Entrevista de discovery

Leé `references/entrevista.md` y seguí el bloque del modo elegido. Reglas generales:

- Máximo **tres rondas de hasta tres preguntas**. Antes de preguntar, explorá el repo y el brief:
  no hagas repetir lo que ya se puede leer en el código, el README o el copy existente.
- Lo primero es siempre el **tipo de producto** (landing / sitio institucional / app web o
  dashboard / e-commerce / portfolio / docs), la **audiencia en situación** y la **única acción**
  que la página tiene que lograr. Después el stack, la marca existente y, crucial, **qué
  imágenes reales existen** (fotos propias, producto, capturas de la interfaz, nada).
- Pedí **páginas modelo** (2 a 4 URLs o capturas) y aclará que es **opcional**: "si tenés sitios
  que te gustan, pasámelos y los analizo; si no, propongo yo la dirección". Pedí también lo
  contrario: uno o dos ejemplos de lo que *no* quiere.
- No pidas colores, tipografías ni "estilo" en abstracto. Eso sale del sujeto y de las
  referencias, no de un formulario. Si el usuario los impone, se respetan y se anotan como fijos.
- En **auditoría**, además: URL o comando para levantar el proyecto, qué tiene que sobrevivir
  (rutas, formularios, datos, SEO, componentes), y si quiere *review* (informe y nada más),
  *restyle* (misma estructura, nueva piel) o *redesign* (se rehace la composición).
- Si el usuario dice "hacé lo que quieras", decidí vos, dejá tus lecturas escritas en el brief y
  seguí. Preguntá solo lo que bloquea el trabajo (por ejemplo, no hay nombre del producto).

## Paso 3 · Análisis de páginas modelo (si las hay)

Si el usuario pasó referencias, leé `references/analisis-referencias.md` y seguí el protocolo
completo: capturás cada sitio a 1440 y 390 px (con `inspect.mjs <url>` de taste-skill si está,
que además te da fuentes cargadas, tamaños y colores medidos; si no, Playwright, Chrome MCP o
`WebFetch` del HTML), mirás las capturas y llenás la ficha por sitio. El resultado es
`design/referencias.md` con:

- lo que las referencias tienen **en común** (eso es lo que el usuario llama "me gusta" sin saber
  nombrarlo: proporción de tipografía, cantidad de color, densidad, tipo de imágenes, ritmo),
- qué **patrones** vale la pena adoptar (composiciones, jerarquía, dispositivos de conversión),
- qué es **de ese sitio y no se copia** (su logo, su foto, su frase, su paleta exacta).

Se extraen patrones y principios, nunca se clona una página. Después del análisis resumíselo al
usuario en cinco líneas y confirmá que leíste bien su gusto antes de seguir.

Sin referencias, esta etapa se reemplaza por la dirección que reparte taste-skill (paso 5) o, si no
está, por el `--design-system` de ui-ux-pro-max más tu propia lista de siete direcciones.

## Paso 4 · El brief

Con la entrevista y las referencias escribís `design/BRIEF.md` siguiendo
`references/brief-template.md`. Es corto (una carilla) y tiene: modo, tipo de producto, audiencia,
acción principal, el **argumento** de la página (una línea por sección: afirmación + prueba),
inventario de lo que solo este sujeto tiene (8 a 12 cosas: su nombre y qué significa, su calle, sus
materiales, sus números, su restricción, sus rituales), imágenes reales disponibles, stack, qué
está fijo (marca, fuentes impuestas), referencias y sus patrones, y lo que queda abierto.

Mostrale el brief al usuario y pedí un OK (una línea alcanza). Si impeccable está instalada,
el bloque de "verdad del producto" del brief se vuelca también a `PRODUCT.md` vía
`/impeccable init` (o lo escribís vos con su plantilla) para que sus otros comandos lo lean.

## Paso 5 · Ejecución según modo

El orden de las skills y los comandos exactos están en `references/orquestacion.md`. En resumen:

**Modo 1 · Proyecto de cero**

1. *Verdad del producto* → `impeccable init` (PRODUCT.md). Sin impeccable: la sección del brief.
2. *Sistema base por tipo de producto* → `ui-ux-pro-max --design-system` para orientarte en
   patrón, tono, anti-patrones de la industria y checklist. Es un piso y un mapa, no el diseño.
3. *Dirección de arte e idea* → taste-skill: inventario, argumento, `draw.mjs` (tres direcciones,
   elegís la que carga algo que solo tiene este cliente), la frase de la idea, el "live thing".
   Si hay referencias, el `design/referencias.md` pesa en la elección de dirección y puede
   justificar un `--redraw` con motivo escrito. Sin taste-skill: la lista de siete direcciones de
   `orquestacion.md` y la tirada manual.
4. *Palabras antes que markup* → copy deck completo (titulares de dos líneas máximo, contenido
   real y completo, nunca pruebas inventadas: sin testimonios, logos ni métricas falsas).
5. *Construir* → tokens → hero → secciones → imágenes reales (propias > generadas > archivos
   abiertos con crédito > dibujadas) → estados → móvil como composición propia. Para pantallas de
   app/dashboard seguí `references/tipos-de-producto.md` § app web y las reglas de app de taste-skill.
6. *Gate* → `lint.mjs` + `inspect.mjs` a 1440/768/390 con 0 FAIL, o Playwright + checklist manual.
7. *Mirar* → crítica sobre capturas con las 14 pasadas y el score de jurado (`references/auditoria.md`
   § crítica). Arreglar los tres problemas más grandes, mirar de nuevo. Tres rondas máximo.
8. *Movimiento* → recién ahora la capa de motion, con `prefers-reduced-motion`.
9. *Cierre* → `impeccable audit` + `impeccable polish` (o la rúbrica técnica de `auditoria.md`),
   y el informe.

**Modo 2 · Auditar / rediseñar**

1. *Registrar el antes* → levantar el proyecto, `inspect.mjs <url> --out design/antes` (con `--app`
   si es pantalla de app), `lint.mjs`, `impeccable audit` + `impeccable critique`, y lectura del
   código (framework, método de estilos, componentes, qué no se puede romper).
2. *Informe* → `design/AUDITORIA.md` con la rúbrica de `references/auditoria.md`: cinco dimensiones
   técnicas (0-4), crítica visual con score, lista de tells detectados, y **las tres cosas que
   más moverían la aguja**, ordenadas por impacto/riesgo.
3. Si el usuario pidió solo *review*, parás acá y entregás el informe.
4. *Restyle o redesign* → se mantiene el stack, el contenido y lo que funciona. Orden de trabajo:
   tipografía → color → marco (márgenes, ritmo, título, heading por sección) → estados → reemplazo
   de componentes genéricos. Con impeccable: `typeset`, `colorize`, `layout`, `harden`, `adapt`.
   Un redesign vuelve al Modo 1 desde el paso 3 con el contenido real.
5. *Probar* → `inspect.mjs --out design/despues`, comparar antes/después a cada ancho, clickear
   todo lo que andaba antes, y reportar medidas lado a lado.

**Modo 3 · Sección o componente**

Heredar tokens, tipografía y composición del entorno. Nada de dirección nueva. Construir, pasar el
gate sobre la página que lo contiene, criticar la captura. Si el entorno es genérico y el usuario
quiere que esto resalte, decíselo: un componente lindo en una página fea se nota más, no menos.

## Reglas de la casa (valen en todos los modos)

Consolidado de las tres skills; el detalle y el porqué están en `references/anti-slop.md`.

- **Titulares de dos líneas o menos a cualquier ancho.** Primero sacá palabras, después ensanchá,
  el tamaño al final.
- **Título claro en la primera pantalla** (un `h1`) y un heading en cada sección. Un extraño tiene
  que saber en cinco segundos qué es esto y qué hacer.
- **Sin eyebrows** (label chiquito arriba del título), **sin numeración decorativa** (01/02/03),
  **sin monospace** fuera de código, **sin tracked caps**, **sin una palabra acentuada** en el
  titular (itálica, serif o color distinto).
- **Sin gradientes, sin sombras en cosas quietas, sin glows, sin glass, sin blobs, sin emojis
  como íconos, sin cards con ícono arriba en fila de tres**, sin hairlines decorativas.
- **Sin paleta de asistente**: crema + terracota, violeta/índigo, negro + un neón. Si el brief la
  pide, se respeta; si el eje quedó libre, no se gasta la libertad ahí.
- **Un ground, una tinta, un acento.** Texto corriente en tinta plena de 16 px o más; el gris es
  para notas secundarias. Dos tipografías como máximo, normalmente una.
- **Márgenes iguales a ambos lados, nada "empujado a un costado", ningún tramo vacío** de más de
  media pantalla. Secciones vecinas con composiciones distintas; ninguna es una grilla de cards.
- **Imágenes reales**: piso de cuatro, idealmente seis a doce. Propias > generadas > archivos
  abiertos con crédito > dibujadas en código. Un gris placeholder es peor que nada.
- **Sacar el ornamento deja espacio: no lo llenes con otro ornamento.** Llenalo con escala, con
  contenido completo o con un campo de color plano.
- **Accesibilidad no negociable**: contraste 4.5:1, foco visible, targets de 44 px, labels
  visibles en formularios, `alt`, teclado, `prefers-reduced-motion`.
- **Nunca se inventa prueba**: ni clientes, ni reseñas, ni logos, ni cifras. Contenido de muestra sí
  (nombres de platos, habitaciones), listado en el informe para que lo confirmen.

Cuando dos skills se contradicen en gusto visual: en páginas (landing, marketing, portfolio,
e-commerce) manda taste-skill; en pantallas de app mandan las reglas de app de taste-skill más las
prioridades UX de ui-ux-pro-max; en lo técnico (a11y, performance, responsive, theming) manda
`impeccable audit`. El brief del usuario le gana a las tres.

## Informe final

No reportes hasta que: el inspector muestre 0 FAIL en los tres anchos sobre la versión final,
hayas abierto todas las capturas después del último cambio, cada sección tenga heading, los
márgenes coincidan y la crítica de la última ronda esté escrita. Después, breve:

- modo y tipo de producto; dirección elegida (nombre y seed si la repartió taste-skill) y cada
  `--redraw` con su motivo;
- la frase de la idea y el "live thing";
- qué referencias se analizaron y qué patrones se adoptaron;
- score de la última crítica y qué queda flojo;
- toda imagen encontrada con título, autor, licencia y fuente, y dónde está su crédito;
- qué imágenes son dibujos o genéricas y deben reemplazarse; qué contenido de muestra hay que
  confirmar; qué quedó sin cablear (checkout, formulario, analítica);
- en auditoría: medidas antes/después lado a lado.

No afirmes un chequeo que no corriste.

## Archivos

| Archivo | Leelo cuando |
|---|---|
| `references/entrevista.md` | Paso 2. Preguntas por modo y por tipo de producto, en el orden en que más cambian el trabajo. |
| `references/analisis-referencias.md` | Paso 3. Protocolo de captura, ficha por sitio, extracción de patrones, qué no copiar. |
| `references/brief-template.md` | Paso 4. Plantilla de `design/BRIEF.md` y su mapeo a `PRODUCT.md`. |
| `references/orquestacion.md` | Paso 5. Orden de las tres skills, comandos exactos, resolución de conflictos y qué hacer sin ellas. |
| `references/tipos-de-producto.md` | Antes de construir. Landing, sitio institucional, app web/dashboard, e-commerce, portfolio: estructura, conversión, patrones UX propios de cada uno. |
| `references/auditoria.md` | Modo 2 y paso 7. Rúbrica técnica (0-4 × 5), las 14 pasadas de crítica, el score de jurado, los caps, el formato del informe. |
| `references/anti-slop.md` | Cuando dudás si algo es una decisión o un default. El registro de tells y con qué se reemplaza cada uno. |
