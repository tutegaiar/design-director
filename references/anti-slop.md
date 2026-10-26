# Anti-slop: el registro de tells

Un *tell* es un dispositivo que hace que una página se lea como generada. Ninguno es mal diseño en
sí; casi todos empezaron como buenas ideas en buenos sitios. Se volvieron tells por producirse por
defecto, en todas partes, sin motivo. Por eso este registro no recomienda una fuente, un color ni un
componente de reemplazo: toda lista publicada de "usá esto en vez de aquello" se convirtió en la
siguiente ola de tells en meses. Los reemplazos son **procedimientos** (derivar del sujeto, repartir
de la librería, decidir una vez), no productos.

Consolidado de taste-skill (`tells.md`, reglas de la casa), impeccable (`craft-floor.md`) y la skill
`frontend-design` de Anthropic. **Prohibido** = el inspector de taste-skill falla la página;
**advertido** = la marca y necesitás un motivo; **default** = no se mide, pero si el eje quedó libre
no se gasta ahí.

## Primera ola (2023–2024)

| Tell | Estado | En su lugar |
|---|---|---|
| Gradientes violeta/índigo en hero, botones y glows | prohibido | la paleta repartida; color plano |
| Titular con texto en gradiente | prohibido | tinta sólida; el énfasis es peso o tamaño |
| Paneles de vidrio: backdrop blur, cards translúcidas | advertido (2 o más) | superficies opacas, un paso de tono del ground |
| Botón "Get started" con glow o gradiente | prohibido | botón plano con el nombre de su acción |
| Sombra gris suave bajo cada card | prohibido | paso de tono, o ninguna caja |
| Tres cards iguales con ícono en cuadradito redondeado | prohibido | el blueprint de sección repartido |
| Emoji como ícono o viñeta | prohibido | palabras, o una imagen real; íconos de una librería real, un solo trazo y peso |
| Titular centrado + subtítulo + dos botones + captura abajo | default | el hero repartido |
| La misma tipografía en toda página generada (Inter, etc.) | advertido | el sistema tipográfico repartido |

## Segunda ola (2025)

| Tell | Estado | En su lugar |
|---|---|---|
| Eyebrow/kicker: label chiquito en mayúsculas trackeadas arriba de cada heading | **prohibido, sin excepción** | metelo en el heading o en la primera frase, o borralo |
| Pill badge arriba del titular ("Nuevo", "Beta", "Presentamos") | prohibido | decilo en la frase de apoyo |
| Una palabra del titular en itálica serif, color o subrayado | advertido | una cara, un color |
| Bento de tiles redondeados como sección de features | advertido como fila de cards | una sección compuesta |
| Fondo casi negro con un neón y glow | prohibido (vía sombra/gradiente) | una paleta oscura repartida, sin glow |
| Navegación flotante en píldora con blur | advertido | una barra plana: wordmark, tres a cinco links, una acción |
| Dashboard falso de barras grises y donas en el hero | default | un fragmento real de la interfaz, o ninguna imagen |
| Punto de estado decorativo ("disponible para trabajar" pulsando) | lint | sacarlo |
| Fade-and-rise en cada sección | default | un solo movimiento firmado |

## Tercera ola (2025–2026): el remedio que se volvió el look

La receta publicada contra las dos primeras olas fue "calentalo y hacelo editorial". Los modelos la
adoptaron entera y hoy es el look generado más reconocible de todos.

| Tell | Estado | En su lugar |
|---|---|---|
| Fondo crema amarillento + acento terracota/óxido/arcilla (≈ #F4F1EA + #D97757) | prohibidos juntos; terracota prohibido solo; crema advertido | la paleta repartida; calidez de una piedra de baja saturación, una tinta profunda, una foto, o un campo cálido entero |
| Serif de alto contraste como atajo a "premium" | default | el sistema repartido, sea de la clase que sea |
| Titular serif itálico enorme | default | como se repartió |
| Cosplay de periódico: hairlines por todos lados, radio cero, columnas densas | prohibido (vía hairline) | estructura por espacio y tono |
| Labels performativos: "Field notes", "Quietly trusted by", "On our desks" | lint | nombres de sección llanos |

## Moda de galería, prohibida como estilo de la casa

Comunes hoy en sitios premiados; en el estudio aparecen *más* en los mejores que en los flojos
(mono 44 % vs 24 %, numeración 38 % vs 21 %). Están prohibidos igual por decisión del autor de
taste-skill: son lo primero que un generador copia de la galería, no llevan información, y una
página sin ellos tiene que encontrar estructura real.

| Tell | Estado | En su lugar |
|---|---|---|
| Micro-labels en monospace, mono como voz "técnica", captions en mono | prohibido | la cara de texto; cifras tabulares para datos; mono **solo** en código real |
| Numeración índice: 01 / 02 / 03, (001), "Paso 02" | prohibido | orden por posición, escala o palabras; `<ol>` si es una lista de verdad |
| Reglas finas: divisores hairline, grillas ruladas, cajas de 1 px | prohibido (cajas: 3 o más) | espacio, pasos de tono, formas llenas, una barra gruesa si la barra es la idea |
| Chrome de herramienta de diseño: cruces, marcas de corte, handles, guías punteadas | prohibido | sacarlo |
| Micro-meta de agencia: hora local, coordenadas, clima, "©2026 — Scroll", cadenas con punto medio (A · B · C) | lint | sacarlo |
| Captions chiquitas en mayúsculas espaciadas esparcidas | prohibido (3 o más) | sentence case legible, junto a lo que describe |

Las mayúsculas trackeadas chicas son el único ítem de este grupo que también condenan los datos:
16 % de los sitios top contra 57 % de los flojos.

## Tells estructurales

| Tell | Estado | En su lugar |
|---|---|---|
| Titular como frase completa a tamaño display, tres o cuatro líneas | prohibido (más de dos) | un título de unas cinco palabras; el resto abajo |
| Orden de stock: hero, logos, features, testimonio, pricing, CTA | default | el orden del argumento |
| Todas las secciones de la misma familia de layout | crítica, pasada 9 | composición distinta por sección |
| Todo centrado | advertido (> 72 %) | anclado a la izquierda, un momento centrado |
| Un radio medio (12–16 px) en todo | default | cuadrado o totalmente redondo, decidido una vez |
| Nueve tamaños de fuente casi iguales | advertido (> 9) | cinco tamaños, bien separados |
| Prueba social inventada: logos, citas, filas de estrellas, "10.000+ equipos" | prohibido por copy | prueba real, o ninguna |
| Texto o caja CSS donde iría una imagen | cap de crítica | una imagen real, o un diseño que no la necesite |
| Cards adentro de cards | default (impeccable: siempre mal) | un contenedor por nivel, o ninguno |
| Borde izquierdo de color > 1 px en cards, ítems, alertas | default | paso de tono, un ícono con sentido, o nada |
| Sombra dura desplazada (`4px 4px 0`) fuera de un mundo realmente neobrutalista | default | el sistema de profundidad del mundo elegido |
| Gris sobre fondo de color | default (impeccable) | secundarios teñidos del matiz de la superficie o de la tinta, nunca gris |
| Negro puro o gris puro | default | tintados con el matiz de la paleta |
| Modal para una tarea que no necesita interrumpir ni proteger el foco | default | en línea, o una página |
| Claro u oscuro elegido por categoría | default | elegido por la escena de uso (quién, dónde, con qué luz) |

## Tells de copy

Marcados por `lint.mjs` de taste-skill: los verbos y adjetivos del género (*unlock, supercharge,
seamless, elevate, effortless, cutting-edge, all-in-one*; en castellano: *potenciá, llevá al
siguiente nivel, soluciones integrales, experiencia única, sin esfuerzo, de vanguardia*); la
corrección ("no es solo X, es Y"); titulares en tricolon; "Get started"/"Learn more" y
"Comenzar"/"Saber más" como labels; más de un puñado de rayas; lorem ipsum; secciones "¿Por qué
elegirnos?" con cuatro bullets que valen para cualquiera.

En su lugar: el botón dice lo que pasa al apretarlo ("Reservar mesa", "Pedir presupuesto", "Ver la
carta"); cada línea solo puede ser de este sujeto; los nombres de sección son llanos ("Precios",
"Preguntas", "Cómo llegar").

## Tells de movimiento

Fade-up idéntico en cada bloque; una docena de entradas escalonadas en el hero; hover que levanta
cada card; easing con rebote (bounce/elastic); loops infinitos que no significan nada; reveals que
fallan y dejan una banda vacía; una sola duración para todas las transiciones; animar `width` o
`height`; sin `prefers-reduced-motion`.

En su lugar: un movimiento firmado hecho bien; entradas por sección escalonadas (heading → texto →
imagen) que no ocultan contenido si falla el script; feedback en cada control; una imagen que se
mueve; ease-out exponencial desde un estado ya visible; solo `transform` y `opacity`.

## Tipografías que significan "dejé de buscar"

No prohibidas: son excelentes fuentes. Pero elegirlas sin un motivo que ninguna otra satisfaga es
el eje libre gastado en el default: **Inter** (sobre todo como display), Space Grotesk, Space Mono,
IBM Plex, DM Sans, DM Serif, Outfit, Plus Jakarta Sans, Instrument Sans, Syne, Fraunces, Playfair
Display, Cormorant, Lora, Crimson, Newsreader. Y las de sistema como display de un mundo propio
(Arial Black, Impact, la sans de la plataforma). La asociación de rubro no es motivo: librería → serif,
tech → mono, infantil → redondeada, son las asociaciones que la lista existe para romper. Elegí la
tipografía como un objeto del mundo del sujeto, en el registro del modo: en Operar/Leer una
workhorse de UI está bien; en Persuadir/Experiencia querés una cara con punto de vista.

## Paletas que delatan

Cuatro looks a los que convergen las interfaces generadas sin importar el sujeto:

1. crema cálido + serif de alto contraste + terracota;
2. casi negro + un neón ácido o bermellón + bordes que brillan;
3. editorial de periódico: hairlines, serif itálico, labels mono chiquitas;
4. tinta plana saturada + cajas negras + sombras duras + display condensada pesada.

Todos legítimos si el brief los pide. Si el eje quedó libre y caíste en uno, el autochequeo falló:
si alguien puede adivinar tu estética solo por la categoría, o por la categoría más la lista de
cosas a evitar, rehacé hasta que ninguna de las dos respuestas sea obvia. Un sujeto librero, cálido o
infantil no ablanda esto: la tela de encuadernar, el hilo, las sobrecubiertas y las guardas cubren
todo el espectro saturado; el papel crema es el rincón más chico de ese mundo.

## Por qué sacar no alcanza

Una página con todos los tells sacados y nada en su lugar es una página vacía con buenos modales, y
eso también es un tell (la "estética de la evitación": cualquiera la adivina desde la categoría más
la lista de prohibiciones). Los tells llenaban el hueco donde debía haber una idea. El orden de
trabajo de la skill existe para llenar ese hueco primero: la idea desde el sujeto, la composición
repartida, imágenes reales o tipografía comprometida, y recién después los chequeos. En los tests
ciegos, una página rica con tells le ganó siempre a una limpia pero delgada.

## Test rápido antes de entregar

Tres preguntas; si alguna da "sí", no está listo:

1. Tapando el logo, ¿esta primera pantalla podría ser del competidor de la otra cuadra?
2. ¿Podría alguien adivinar la paleta y la tipografía sabiendo solo el rubro?
3. ¿Hay algún elemento que esté ahí porque "las páginas tienen eso" y no porque este sujeto lo pida?
