# Tipos de producto

Cada superficie tiene un **modo**: qué significa que al visitante le fue bien ahí. El modo decide
cuánta ambición visual corresponde y dónde se gasta.

| Modo | El visitante… | Superficies | La ambición se nota en |
|---|---|---|---|
| **Persuadir** | decide y actúa | landing, marketing, pricing, campaña, home de e-commerce | composición audaz, idea propia, imágenes grandes, una pieza firmada |
| **Operar** | completa una tarea | app web, dashboard, admin, checkout, settings, backoffice | precisión y contención: escaneabilidad, consistencia, patrones que ya conoce; la marca vive en los detalles |
| **Leer** | entiende algo | docs, blog, guías, institucional informativo | estructura para comprender; la tipografía es el diseño |
| **Experiencia** | está dentro de la obra | portfolio, galería, showcase | el trabajo lidera desde la primera pantalla, la interfaz se retira |

El modo es de la **superficie**, no del producto: la landing de un SaaS es Persuadir, su app es
Operar, sus docs son Leer. Un producto con las tres se construye tres veces con una sola paleta y
tipografía compartidas.

---

## Landing / página de producto (Persuadir)

**Qué la hace funcionar**: continúa la frase del anuncio o del mensaje que trajo al visitante;
responde en la primera pantalla *qué es, para quién, qué hago*; tiene una idea que solo puede ser
de este sujeto; prueba cada afirmación con algo real; un solo botón que dice lo que hace.

**Estructura**: sale del **argumento** del brief, no de una plantilla. Cada sección es una
afirmación con su prueba; sin afirmación no hay sección. Esto es lo que evita la secuencia de
stock *hero → logos → tres features → testimonio → pricing → CTA*. Roles disponibles (los de
`draw.mjs --list roles`): features, showcase, how-it-works, testimonial, proof, stats, pricing,
faq, cta, footer, intro, about, work, gallery, list, contact.

**Primera pantalla**: titular ≤ 2 líneas (~5 palabras, ~32 caracteres es la mediana de los sitios
premiados); una frase de apoyo justo debajo que diga en llano qué es la cosa si el titular es un
nombre o una figura; un botón real; y la imagen más característica del mundo del sujeto, grande
(≥ 40 % de la pantalla si existe una foto o un video propio). Para un evento: qué, cuándo y dónde
en tipo grande. Para un producto: qué es y qué cuesta o qué hace.

**Prueba**: solo real. Clientes, reseñas, prensa, cifras, logos: si no existen, la sección no
existe. La alternativa honesta a un testimonio inventado es mostrar el producto funcionando, el
proceso, el lugar, el detalle del material.

**Live thing**: una cosa que el visitante puede hacer, hecha de la idea y del contenido real:
elegir una madera y ver la silla, poner su nombre y verlo cortado en las letras de la fundición,
mover el monto y leer la cuota, ver si el local está abierto ahora. Una sola, que ande con el
pulgar, con fallback sin script.

**Argentina/LatAm**: el CTA suele ser WhatsApp (`https://wa.me/549...?text=...` con asunto
prellenado), no un formulario; el precio en pesos con cuotas y medio de pago visibles baja la
objeción principal; horario y ubicación con mapa real para negocios físicos.

**Tells específicos**: hero centrado con eyebrow + tres cards con ícono + franja de logos grises
+ sección "¿Por qué elegirnos?" con cuatro bullets genéricos + testimonios con avatares de stock.

---

## Sitio institucional (Leer + Persuadir)

Varias páginas, un visitante que busca algo concreto (horario, inscripción, quiénes son, cómo
llegar). La home persuade; las interiores informan.

- **Sitemap mínimo** antes de diseñar: qué páginas, cuál es la que más visitas recibe (suele ser
  "contacto" o "inscripciones", no la home), qué puede hacer el visitante en cada una.
- **La home** tiene una idea y una primera pantalla como una landing, pero su trabajo es
  **derivar**: tres o cuatro puertas claras a lo que la gente viene a buscar.
- **Interiores**: tipografía de lectura (16–20 px, 45–75 caracteres por línea, interlineado
  1.45–1.6), títulos que nombran la página, navegación que siempre dice dónde estás, contacto al
  alcance en todas.
- **Contenido que envejece**: fechas, aranceles, autoridades, plantel. Decidí con el usuario quién
  lo mantiene; si nadie, ese dato no va o va con "consultar".
- **Colegios, ONGs, estudios, consultorios**: la prueba es el lugar, la gente real y la historia,
  no stock. Una buena foto del patio vale más que diez íconos de "valores".
- **Accesibilidad** pesa más que en una landing: público amplio, mayores, lectores de pantalla.
  Contraste, tamaños, foco, estructura de headings real.

---

## App web / dashboard / admin (Operar)

Acá la ambición es **no estorbar**. La persona lo usa horas; lo que en una landing es firma, acá
es ruido. taste-skill tiene un run propio (`references/app-screens.md`, `draw.mjs --app`,
`inspect.mjs --app`); leelo entero si está instalada.

**Pregunta de la pantalla**: cada pantalla responde una pregunta ("¿qué tengo que atender hoy?",
"¿cómo viene el mes?", "¿quién está de licencia esta semana?"). Si no podés escribirla, la pantalla
no está diseñada.

**Lo que separa una pantalla de producto real de una generada**:
- paneles quietos: bordes de 1 px en tono vecino o separación por fondo, sin sombras, sin glass,
  sin gradientes, sin íconos en cuadraditos de color;
- el color se gasta en los **datos** (estados, series, lo que pide decisión), no en la cáscara;
- cifras alineadas (tabular figures), unidades, períodos y comparaciones honestas; nada de
  "+12 %" inventado ni totales de vanidad;
- gráficos que responden la pregunta: un hallazgo enunciado en texto al lado; sin arcoíris, sin
  donas decorativas, sin sparklines de relleno;
- tablas reales: encabezados, orden, filtros que se ven aplicados, densidad acorde a la frecuencia
  de uso, filas clickeables con área completa;
- **estados**: vacío (con la acción para salir de él), cargando (esqueleto que reserva el
  espacio), error (qué pasó y cómo seguir), sin permisos, parcial; el primer uso y el día mil se
  diseñan los dos;
- **formularios**: label visible arriba, ayuda al lado del campo, error junto al campo y resumen
  arriba, validación en vivo sin castigar mientras se escribe, un botón primario por pantalla,
  teclado completo, `aria-describedby` para límites;
- **navegación**: lateral plegable o superior, ≤ 5 destinos principales, siempre se sabe dónde se
  está; en móvil la navegación se guarda y la pantalla se recompone (no es el desktop apretado).

**Densidad**: quien usa esto 8 horas quiere ver más por pantalla (espaciado 8–32 px, cuerpo 14–15
px es aceptable acá); quien entra una vez al mes quiere guía. Preguntalo (`entrevista.md`).

**Librerías**: si el proyecto ya tiene shadcn, MUI, Vuetify, Nuxt UI, se heredan sus componentes y
se trabaja con tokens; no se reinventa un botón. ui-ux-pro-max tiene guías por stack
(`--stack shadcn`, `--stack react`, `--domain chart`).

**Gate**: `inspect.mjs --app` si taste-skill está; impeccable `audit` con la dimensión de
integridad; prueba con teclado de punta a punta.

---

## E-commerce (Persuadir en home/PDP, Operar en carrito/checkout)

Una tienda es el tipo donde más decide el **activo**: fotos de producto consistentes (mismo fondo,
misma luz, mismo recorte) valen más que cualquier dirección de arte. Si no hay, la primera
recomendación del informe es conseguirlas; la composición se elige para que no dependa de lo que
no existe.

**Plataforma primero**: Tienda Nube, WooCommerce, Shopify, Mercado Libre como canal, o propio. En
una plataforma se diseña el **tema** y se respeta su checkout (no se rehace); en propio hay que
diseñar y probar todo el flujo. La pasarela (Mercado Pago u otra) impone sus botones y sellos.

**Home**: una idea del sujeto (la marca, su taller, su barrio, su material) + puertas a categorías
+ un producto o colección protagonista. No una grilla de 40 productos de entrada.

**Listado / categoría (PLP)**:
- tarjeta de producto con lo esencial: foto en recorte único, nombre, precio (con cuotas o
  promoción si aplica, sin que el tachado sea más grande que el precio), variantes disponibles
  (muestras de color), estado (sin stock, últimas unidades) y un solo gesto para entrar;
- filtros visibles y combinables, con el estado aplicado a la vista y un "limpiar"; orden
  explícito; cantidad de resultados; en móvil, filtros en un panel que no pierde la posición;
- paginación o "ver más" que mantiene el scroll; nunca scroll infinito sin footer alcanzable.

**Ficha de producto (PDP)**:
- galería con zoom real y miniaturas; la primera foto es el producto, no un lifestyle;
- título, precio y **el botón de compra visibles sin scroll** en desktop, y **pegado abajo en
  móvil** (sticky) cuando la galería lo tapa;
- variantes como controles reales (talle, color) con el estado de stock por variante; si falta
  una, se ve y se puede pedir aviso;
- envío y retiro con costo y plazo **antes** del carrito (es la objeción número uno); cambios y
  devoluciones en una línea; medios de pago y cuotas;
- descripción completa: medidas, materiales, cuidado, origen; una tabla de talles real si aplica;
- reseñas solo si son reales; sin reseñas no hay sección de reseñas;
- productos relacionados al final, no antes del botón.

**Carrito**: editable (cantidad, quitar, variante), total con envío estimado o calculadora por
código postal, código de descuento sin que sea un cartel que invite a irse a buscar uno,
seguir comprando y pagar sin ambigüedad.

**Checkout** (Operar, el más estricto):
- invitado por defecto; crear cuenta es opcional y después;
- pasos visibles con progreso, o una sola página larga; el total siempre a la vista;
- formulario mínimo: autocompletar dirección, CP primero si calcula envío, un campo de nombre,
  teléfono con formato local, sin pedir dos veces lo mismo;
- errores junto al campo, en el idioma del cliente, con cómo corregir;
- resumen del pedido antes de pagar; sellos y medios de pago reales; sin ventanas emergentes;
- confirmación con número, qué sigue y cómo seguir el envío; mail que diga lo mismo.

**Transversal**: búsqueda con sugerencias y tolerancia a errores; página de "no hay resultados"
con salidas; precios siempre con moneda y por qué cambian (promo, cuotas); "sin stock" visible
antes de clickear; velocidad (imágenes WebP/AVIF, lazy, espacio reservado para evitar saltos);
WhatsApp como canal de consulta en el PDP cuando el rubro lo pide.

**Tells específicos**: banner carrusel automático con tres promos que nadie lee; pop-up de
descuento al entrar; tarjetas con sombra y hover que crece; precio tachado gigante; "¡Oferta!" en
rojo sobre todo; fotos de stock que no son el producto.

---

## Portfolio / galería (Experiencia)

- El **trabajo abre**: la primera pantalla es la pieza más fuerte, grande, no un titular sobre el
  autor. El nombre y qué hace, sí, pero al servicio de la pieza.
- Cada proyecto con su propia composición y **detalle real** (contexto, rol, resultado, piezas);
  un portfolio de miniaturas iguales es un listado, no una experiencia.
- Si el trabajo es inventado para el brief, se dibuja cada pieza como un *still* terminado de ese
  trabajo (su tarjeta de título con su tipografía, su afiche), nunca como un pictograma.
- La interfaz se retira: navegación mínima, cursor y transiciones que acompañan, contacto donde
  termina de mirar. Si busca trabajo o clientes, el contacto es una acción clara, no un footer.

---

## Docs / blog (Leer)

- Estructura antes que estilo: jerarquía de headings real, tabla de contenidos, búsqueda,
  breadcrumbs, prev/siguiente, versión si aplica.
- Tipografía de lectura larga: 16–18 px, 60–75 caracteres, interlineado generoso, código en
  monospace **solo** en bloques de código (ahí sí corresponde), tablas con líneas (ahí también).
- Bloques de ejemplo copiables, advertencias distinguibles sin depender del color, modo oscuro
  cuidado si el público lee de noche.
- Una página de docs no es una landing: nada de hero con CTA.

---

## Híbridos

SaaS con landing + app: la landing muestra la app con **fragmentos reales de la interfaz**
(construidos con las reglas de app, datos que suman, un hallazgo enunciado), recortados como la
dirección trata una imagen. Un dashboard de barras grises es la imagen más débil que puede tener
una página de software; uno que parece un producto andando es la más fuerte. Se construyen con dos
runs y una sola paleta y tipografía.
