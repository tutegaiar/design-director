# Orquestación de taste-skill, ui-ux-pro-max e impeccable

## Qué es cada una, en una línea

| Skill | Naturaleza | Fuerte en | Floja en |
|---|---|---|---|
| **ui-ux-pro-max** | base de datos buscable + motor de reglas (Python, sin dependencias) | orientarse rápido por tipo de producto: patrón de landing, estilo, paleta, par tipográfico, anti-patrones de la industria, 119 guías UX, 22 stacks, charts, a11y | no construye ni mira el resultado; sus estilos sugeridos a veces traen sombras suaves, glass o gradientes que las otras dos prohíben |
| **taste-skill** (`design-taste-frontend`) | método de dirección de arte + inspector en Chrome real (Node 22+) | que la página pertenezca a *este* sujeto: inventario, argumento, tres direcciones repartidas de una librería de 247 sitios premiados, la frase de la idea, fotos reales de archivos abiertos con crédito, reglas de la casa medidas por `inspect.mjs`, crítica de jurado | es lenta y cara (30–45 min, cientos de miles de tokens por página); muy opinada: si el brief pide gradientes o glass, hay que pasarle `--allow` |
| **impeccable** | suite de 24 comandos + detector determinístico de 62 reglas | el principio (`init` → `PRODUCT.md`, `shape`) y el final (`audit`, `critique`, `polish`, `harden`, `adapt`, `optimize`); refinamientos puntuales (`typeset`, `layout`, `colorize`, `quieter`, `bolder`); modos persuadir/operar/leer/experiencia | su flujo de "concept-seed" y páginas de decisión es pesado; para la dirección de arte de una landing, taste-skill da mejor resultado |

Son complementarias porque atacan tres momentos distintos: **decidir** (ui-ux-pro-max),
**construir con punto de vista** (taste-skill) y **asegurar calidad** (impeccable). El error
común es correr las tres sobre el mismo paso y que se peleen.

## El orden (proyecto de cero)

```
 brief (esta skill)
   │
   ├─ 1. impeccable init ──────────────► PRODUCT.md        verdad del producto, sin estética
   │
   ├─ 2. ui-ux-pro-max --design-system ► design/base.md    patrón · estilo · paleta · tipo ·
   │                                                       anti-patrones · checklist  (es un MAPA)
   │
   ├─ 3. taste-skill: inventario → argumento → draw.mjs (3 direcciones) → idea → copy deck
   │       + design/referencias.md pesa en la elección de dirección
   │
   ├─ 4. construir (tokens → hero → secciones → imágenes → estados → móvil)
   │       ui-ux-pro-max --domain ux / --stack para dudas puntuales de implementación
   │
   ├─ 5. gate: lint.mjs + inspect.mjs (0 FAIL a 1440/768/390)
   ├─ 6. mirar: crítica de 14 pasadas + score  ×3 máx
   ├─ 7. motion
   │
   └─ 8. impeccable audit → polish → (harden si va a producción) → informe
```

Por qué este orden y no otro:

- `init` primero porque `PRODUCT.md` lo leen después `audit`, `critique` y `polish`: sin él,
  impeccable te va a ofrecer correr `init` en medio del cierre.
- `--design-system` **antes** de `draw.mjs` porque es barato (segundos) y te dice en qué cuadrante
  estás: qué patrón de conversión usa esta industria, qué evita, qué par tipográfico es razonable,
  qué checklist aplica. Con eso leés mejor las tres direcciones que reparte taste-skill. Si lo
  corrés después, lo único que hace es contradecir una decisión ya tomada.
- `draw.mjs` **adopta** la dirección repartida; el design-system de ui-ux-pro-max se usa para
  justificar un `--redraw` solo si hay un motivo que podés escribir (la paleta pelea con el
  material del sujeto, la sección no puede sostener el contenido real), nunca para volver a la
  composición que hubieras hecho igual.
- `audit`/`polish` al final porque juzgan la página construida; corridos antes, auditan un esqueleto.

## Comandos exactos

Rutas: `<taste>` = carpeta de taste-skill (contiene `scripts/draw.mjs`), `<uupm>` = carpeta de
ui-ux-pro-max (contiene `scripts/search.py`), `<imp>` = carpeta de impeccable (contiene
`scripts/impeccable`). Encontralas en el paso 0 de la skill. Corré todo desde la raíz del proyecto.

### 1. impeccable init

```
/impeccable init
```

Explora el repo, pregunta solo los huecos materiales (usuario, situación, mecanismo diferencial,
restricciones) y escribe `PRODUCT.md`. Ya tenés el brief: respondé las preguntas de `init` con el
brief y no lo hagas repetir al usuario. Si `init` pregunta por el stack en greenfield, la
respuesta está en *Fijos*. `init` **no** pide estética: no se la des.

Sin impeccable: escribí `PRODUCT.md` vos con la plantilla de `brief-template.md` § mapeo.

### 2. ui-ux-pro-max --design-system

```bash
python "<uupm>/scripts/search.py" "<tipo de producto> <rubro> <2–3 palabras clave>" \
  --design-system -p "<Nombre del proyecto>" --persist --output-dir .
```

- Ejemplos de query: `"bakery neighborhood local shop warm"`, `"B2B analytics dashboard internal"`,
  `"fashion ecommerce small brand"`, `"school institutional parents enrollment"`.
- Deja `design-system/<slug>/MASTER.md`. Copiá lo útil a `design/base.md`: el **patrón** de
  página (orden de secciones y dónde va el CTA), los **anti-patrones** de la industria, el
  **checklist** de pre-entrega. Tratá paleta y par tipográfico como *una opción razonable*, no
  como la decisión: la decisión la toma la dirección del paso 3.
- Dials opcionales: `--density 8` para dashboards, `--variance 2` para algo quieto, `--motion 3`
  para casi nada de animación.
- Consultas puntuales durante la construcción, una intención por query, 2–5 términos:
  `"error summary validation" --domain ux` · `"product card price variants" --domain ux` ·
  `"sticky add to cart mobile" --domain ux` · `"chip badge overflow" --stack html-tailwind` ·
  `"suspense streaming" --stack nextjs` · `"real-time dashboard" --domain chart`.
- Si devuelve 0 resultados, reintentá una vez más angosto; si sigue vacío, decí que la
  recomendación es un default general, no un match.

Sin ui-ux-pro-max: usá `tipos-de-producto.md` de esta skill para el patrón y los anti-patrones.

### 3. taste-skill: dirección e idea

Leé **entero** el `SKILL.md` de taste-skill antes de este paso (es largo y cambia entre
versiones; lo de abajo es el resumen para que sepas qué viene).

```bash
# ¿página o pantalla de app?  Página → run normal.  App → references/app-screens.md y --app.
node <taste>/scripts/draw.mjs --list sectors        # saas dev-tool ai-product consumer-app finance
                                                    # agency studio-portfolio personal-portfolio
                                                    # ecommerce physical-product fashion hospitality
                                                    # restaurant real-estate architecture event
                                                    # health education nonprofit culture music other
node <taste>/scripts/draw.mjs --list roles          # features showcase how-it-works testimonial proof
                                                    # stats pricing faq cta footer intro about work
                                                    # gallery list contact   (el hero va implícito)

# Tres direcciones para elegir (las secciones salen del ARGUMENTO del brief, en su orden):
node <taste>/scripts/draw.mjs --sector <sector> --brief "<una línea del sujeto>" \
  --sections <roles en el orden del argumento> [--have photography,product-photo,product-ui,illustration,video] \
  [--keep palette,type] [--tone quiet|bold|warm|technical|playful|luxury|editorial] --options 3

# Elegida una (la que carga algo del inventario, no la más familiar), la hoja completa:
node <taste>/scripts/draw.mjs <mismos args sin --options> --direction <id>

# Pantallas de app:
node <taste>/scripts/draw.mjs --app --kind <finance|wallet|commerce|analytics|devtools|builder|creator|smb-admin|workspace|community|support|markets|report> --brief "<producto>"
```

- `--have` solo con activos que **realmente existen** (los de archivos abiertos no cuentan).
- `--keep palette,type` cuando la marca ya fija colores o fuentes (*Fijos* del brief).
- Con `design/referencias.md`: evaluá las tres direcciones también contra el patrón común de las
  referencias. Si una dirección carga el patrón común **y** algo del inventario, es esa. Si
  ninguna, `--redraw direction` **una vez**, con el motivo escrito en el brief.
- Después de la hoja: la frase de la idea ("En esta página, **X del sujeto** se convierte en
  **Y**"), el test del competidor, y el *live thing*. Sin las dos frases llenas desde el sujeto no
  se empieza a construir.
- Copy deck completo en texto plano antes de cualquier markup (titulares ≤ 2 líneas a todo ancho,
  ~32 caracteres es seguro; una frase de apoyo debajo; un botón real; contenido completo).

Imágenes:

```bash
node <taste>/scripts/assets.mjs "<query del inventario, no de la categoría>"   # Openverse, Wikimedia, Met, AIC
node <taste>/scripts/assets.mjs --get <ref>                                    # descarga + fuente + licencia
node <taste>/scripts/assets.mjs --video "<query>"                              # un clip mudo en loop
node <taste>/scripts/assets.mjs --credits                                      # línea de créditos del footer
```

Sin taste-skill, la dirección a mano (es lo que hace la skill por dentro):

1. Escribí la **página que esta categoría siempre hace** y su **opuesto predecible**. Las dos son
   la rutina; quedan afuera.
2. Del mundo del sujeto (su inventario, sus tradiciones gráficas, sus lugares, sus objetos
   impresos, cómo se veía su rubro antes de la web) listá **siete direcciones concretas**, cada
   una con: una línea de por qué resuena, su ground y colores principales, su voz tipográfica, su
   firma reconocible. Al menos tres familias de material distintas.
3. Tirá un dado honesto (`shuf -i 1-7 -n 3` o `node -e "..."`) y presentale al usuario esas
   **tres**, con igual peso, más una "salida estándar" (la convención del rubro bien hecha, sin
   ironía) por si la prefiere. Elegí con él. Que el dado reparta es lo que evita que caigas siempre
   en la primera de la lista.
4. Comprometé la elegida: estrategia de color (contenida / comprometida / paleta / empapada),
   claro u oscuro por escena de uso (quién, dónde, con qué luz), una o dos tipografías elegidas
   como objetos de ese mundo (no las de siempre: Inter, Space Grotesk, Playfair, DM Sans, Syne,
   Plus Jakarta…), primera pantalla descripta con precisión, firma de interacción.
5. Lo anotás en el brief § Dirección.

### 4. Construir

Orden de trabajo de taste-skill, que vale con o sin ella: tokens → hero exacto al blueprint a
desktop y a 390 → cada sección con su blueprint y contenido real (vecinas distintas) → imágenes
en orden de preferencia → el live thing → plenitud (cada pantalla de desktop es un póster) → el
marco (márgenes iguales, título, heading por sección) → estados y semántica (links y botones
reales, foco, alt, teclado). Motion **después** del gate, no ahora.

Si taste-skill está: `<taste>/assets/base.css` es una base neutra (reset, tokens, pasos fluidos de
tipo, grilla, foco) sin look propio; `assets/app.css` y `assets/charts.js` para pantallas de app.

Si impeccable está: leé `<imp>/reference/craft-floor.md` justo antes de tocar UI. Tiene el piso de
calidad (contraste, profundidad, espaciado, tipo, estados, superficies del navegador: selección,
caret, scrollbar, foco) y los defaults que hay que reescribir en vez de suavizar.

### 5. Gate

```bash
node <taste>/scripts/lint.mjs <carpeta de fuentes>              # patrones y frases prohibidas en el código
node <taste>/scripts/inspect.mjs <url o index.html>             # 1440 / 768 / 390, FAIL/WARN, capturas
node <taste>/scripts/inspect.mjs <url> --app                    # para pantallas de app
node <taste>/scripts/inspect.mjs <url> --allow <regla>          # solo para un fijo del brief, dicho en el informe
```

Arreglá cada FAIL; cada WARN es un error salvo que lo puedas defender en una frase. Con build step,
el último gate sobre el **build de producción** (`vite build && vite preview`, `next build && next
start`), no sobre el dev server.

Sin taste-skill: Playwright a los tres anchos y el checklist de `auditoria.md` § gate manual.

### 6. Mirar

Abrí **todas** las capturas que listó el inspector. Crítica con las 14 pasadas y el score de
`auditoria.md`. Arreglá los tres problemas más grandes. Repetí. Tres rondas como máximo. Se juzgan
las imágenes: si algo se ve mal en la captura es real, diga lo que diga el código.

### 7. Motion

Capa de movimiento recién ahora: una firma, entradas escalonadas por sección (heading → texto →
imagen, 60–90 ms, 16–32 px), feedback en cada control, una imagen que se mueve. Solo `transform` y
`opacity`; todo con fallback `prefers-reduced-motion` que conserva el contenido. Nada que quede
oculto si falla el script.

### 8. Cierre con impeccable

```
/impeccable audit <target>      # técnico: a11y, performance, theming, responsive, integridad (0-4 cada uno)
/impeccable critique <target>   # UX: jerarquía, claridad, resonancia; con puntaje heurístico
/impeccable polish <target>     # pase final y alineación con el sistema
/impeccable harden <target>     # errores, i18n, overflow de texto, edge cases — si va a producción
/impeccable adapt <target>      # si el móvil quedó como desktop apretado
```

El detector de impeccable y `inspect.mjs` miden cosas parecidas con criterios distintos. Si uno
marca algo que el otro no, leé el hallazgo en contexto y decidí; no ignores a ninguno por sistema.

Sin impeccable: la rúbrica técnica de `auditoria.md` (cinco dimensiones 0–4) a mano, y Lighthouse
(`npx lighthouse <url> --only-categories=accessibility,performance,best-practices`) si hay Chrome.

## Orden en auditoría (modo 2)

```
 1. antes:  inspect.mjs <url> --out design/antes  ·  lint.mjs  ·  impeccable audit + critique
            + lectura del código (framework, método de estilos, componentes, qué sobrevive)
 2. informe: design/AUDITORIA.md  (rúbrica técnica + crítica + tells + top 3 por impacto/riesgo)
 3. review → fin.   restyle/redesign →
 4. ui-ux-pro-max --design-system (--keep lo que la marca fije) para el mapa del rubro
 5. restyle: tipografía → color → marco → estados → componentes genéricos reemplazados
            con impeccable: typeset → colorize → layout → harden → adapt, en ese orden
    redesign: taste-skill desde "argumento" con el contenido real y la misma stack
 6. después: inspect.mjs --out design/despues  ·  comparar a cada ancho  ·  clickear todo lo que andaba
 7. impeccable audit (de nuevo) → polish → informe con medidas antes/después
```

Nunca se migra de framework ni de librería de estilos en una auditoría. Revisá el archivo de
dependencias antes de agregar nada.

## Resolución de conflictos

| Conflicto típico | Quién manda | Por qué |
|---|---|---|
| ui-ux-pro-max sugiere "Soft UI / glassmorphism / sombras suaves" y taste-skill lo prohíbe | **taste-skill** en páginas | las reglas de la casa están medidas contra 247 sitios: los premiados usan sombras en reposo 24 % vs 48 % de los flojos |
| ui-ux-pro-max dice "mínimo 44 px de target" y taste-skill no lo mide | **ui-ux-pro-max / impeccable audit** | lo técnico-accesible siempre se cumple; taste-skill no lo contradice, solo no lo mide |
| taste-skill pide "al menos cuatro imágenes reales" en un dashboard | **reglas de app** de taste-skill (`app-screens.md`) | el piso de imágenes es de páginas; una pantalla de app muestra datos reales, no fotos |
| impeccable `critique` quiere "más personalidad" y taste-skill ya repartió una dirección quieta | **el brief / la dirección elegida** | una dirección adoptada se ejecuta a fondo; "más personalidad" no es un hallazgo, es gusto |
| el usuario pide un gradiente / una fuente de la lista negra / un eyebrow | **el usuario** | se anota como fijo en el brief, `--allow` en el inspector, y se dice en el informe |
| dos herramientas dan medidas distintas de contraste | **la peor** | si una falla, falla |

Regla general: en **páginas** manda taste-skill en gusto, impeccable en técnica, ui-ux-pro-max
informa. En **pantallas de app** mandan las reglas de app de taste-skill + prioridades UX de
ui-ux-pro-max, impeccable en técnica. El brief del usuario les gana a las tres.

## Instalación (para pasarle al usuario si falta alguna)

```bash
# taste-skill (Node 22+, Chrome/Edge/Chromium instalado; sin API keys)
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
#   o como plugin de Claude Code:
/plugin marketplace add Leonxlnx/taste-skill
/plugin install taste-skill@taste-skill

# ui-ux-pro-max (Python 3, sin dependencias)
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
#   o:  npm i -g ui-ux-pro-max-cli && uipro init --ai claude --global

# impeccable (binario autocontenido; se descarga en el primer uso)
npx impeccable install          # desde la raíz del proyecto; después /impeccable init
#   o:
/plugin marketplace add pbakaus/impeccable   → /plugin → instalar Impeccable
```

Las tres se actualizan seguido y cambian flags y rutas. Si un comando de arriba falla, leé el
`SKILL.md` de esa skill tal como está instalado y seguilo; esta referencia resume, no reemplaza.
