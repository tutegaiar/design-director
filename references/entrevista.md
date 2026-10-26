# Entrevista de discovery

Un buen brief no es un formulario largo: es saber las cuatro o cinco cosas que cambian el trabajo y
no preguntar el resto. Las que más cambian el trabajo son siempre las mismas: **para quién, en qué
situación, qué tiene que lograr la página, con qué material real contamos, y qué no se puede tocar.**

Reglas:

- Explorá antes de preguntar (repo, README, copy existente, `package.json`, assets en `/public`).
  Lo que ya se lee no se pregunta; se confirma en una línea ("veo que es Next + Tailwind, ¿sigue?").
- Máximo tres rondas, máximo tres preguntas por ronda. Agrupá por tema. Primero las que más
  cambian el trabajo.
- Usá `AskUserQuestion` con opciones cuando la pregunta tenga opciones naturales (tipo de producto,
  modo, stack); pregunta abierta para audiencia, acción y material.
- No preguntes colores, tipografías ni "estilo". Preguntá por el sujeto y por referencias. Si el
  usuario impone un color o una fuente, se anota como **fijo** y no se discute.
- Confirmá tus inferencias, no las des por aprobadas.
- Las referencias son **opcionales**. Formulación sugerida: "¿Tenés dos o tres sitios que te
  gusten, aunque sean de otro rubro? Los analizo y saco los patrones. Si no, propongo yo la
  dirección." Y pedí también un ejemplo de lo que no quiere: eso suele ser más informativo.

## Ronda 1 — común a todos los modos

1. **Modo**: proyecto de cero / auditar o rediseñar algo existente / una sección o componente.
2. **Tipo de producto**: landing o página de producto · sitio institucional (varias páginas:
   quiénes somos, servicios, contacto) · app web o dashboard (se *usa*, no se *lee*) · e-commerce ·
   portfolio o galería · documentación o blog. Si es híbrido (producto SaaS con landing y app), se
   anotan los dos y cada superficie se trata con su modo.
3. **Una línea sobre el sujeto**: qué es, quién está detrás, dónde está. Si falta el nombre, es la
   única pregunta que bloquea.

## Ronda 2 — por modo

### Modo 1 · Proyecto de cero

- **Audiencia en situación**: quién llega, desde dónde (un anuncio, un QR en el local, un link de
  WhatsApp, Google), sabiendo qué, y en qué dispositivo (si es un local de barrio, es un celular).
- **La única acción**: qué tiene que hacer el visitante cuando termina (reservar, comprar, pedir
  presupuesto, descargar, registrarse, llamar). Una sola. Si dice "varias", preguntá cuál sería la
  que, si fuera la única, igual valdría la pena hacer la página.
- **La objeción principal**: qué duda frenaría a esa persona (precio, confianza, distancia,
  "¿será para mí?").
- **Material real**: fotos propias (del local, del producto, del equipo), capturas de la interfaz,
  logo, textos existentes, videos. Esta pregunta es la que más decide la calidad final: no se
  planifica alrededor de imágenes que no existen. "Nada" casi nunca es nada: la ciudad, la calle,
  los materiales, la historia del rubro están en archivos abiertos.
- **Stack y deploy**: si el repo no lo dice, preguntá una vez: HTML/CSS estático, un framework
  concreto, o que recomiendes vos; y dónde se publica (Vercel, hosting compartido, WordPress,
  servidor propio). Anotá "delegado: X" si lo deja en tus manos.
- **Marca existente**: logo, colores o fuentes ya definidas (fijos) o nada.
- **Referencias** (opcional): 2–4 URLs o capturas que le gusten, y 1–2 que no.

### Modo 2 · Auditar / rediseñar

- **Dónde está**: URL pública, o cómo levantarlo local (comando, puerto). Credenciales de prueba si
  hay login.
- **Qué alcance quiere**: *review* (informe y recomendaciones, sin tocar nada) · *restyle* (misma
  estructura y componentes, nueva piel: tipo, color, espaciado) · *redesign* (se rehace la
  composición; sobrevive el contenido, la función y el stack).
- **Qué tiene que sobrevivir sí o sí**: rutas, formularios, integraciones, datos, SEO, componentes
  compartidos con otras partes, tracking.
- **Qué le molesta hoy** en sus palabras, y qué le gusta y no quiere perder. Anotalo textual.
- **Qué páginas o pantallas** entran (home sola, el flujo de compra entero, el dashboard principal).
- **Material real** y **marca**: igual que en Modo 1.
- **Referencias** (opcional).

### Modo 3 · Sección o componente

- Qué sección/componente, dónde vive (archivo, ruta) y qué tiene que hacer.
- Si el proyecto tiene tokens o design system documentado (`DESIGN.md`, `tailwind.config`,
  variables CSS) — se hereda, no se pregunta estética.
- Qué contenido real va adentro.
- Si quiere que *resalte* o que *desaparezca* en el entorno.

## Ronda 3 — por tipo de producto (solo lo que falte)

### Landing / página de producto
- Fuente de tráfico y promesa del anuncio o mensaje que trae al visitante (la página tiene que
  continuar esa frase, no empezar de cero).
- Precio o modelo (se muestra o no, hay planes o es presupuesto).
- Prueba real disponible: clientes, casos, prensa, números verificables. Si no hay, se diseña sin
  prueba; no se inventa.

### Sitio institucional
- Lista de páginas (sitemap mínimo) y cuál es la que más importa.
- Qué tiene que poder hacer el visitante en cada una (contacto, turnos, inscripción, descarga).
- Quién mantiene el contenido después (eso decide CMS vs. estático).

### App web / dashboard
- La tarea principal y con qué frecuencia se hace (diaria, pico mensual).
- Qué datos reales se muestran (campos, volúmenes, rangos) y de dónde salen; cómo se ven los
  estados vacío, cargando, error, sin permisos.
- Roles y densidad: quién lo usa 8 horas por día quiere densidad; quien entra una vez al mes
  quiere guía.
- Si hay componentes/librería ya adoptados (shadcn, MUI, Vuetify): se heredan.

### E-commerce
- Catálogo: cuántos productos, categorías, variantes (talle, color), stock variable, precios con
  promociones o cuotas.
- Plataforma (Tienda Nube, WooCommerce, Shopify, Mercado Libre como canal, propio) y pasarela
  (Mercado Pago, otra). Si ya está decidido, define muchísimo.
- Logística: envío, retiro en local, zonas; políticas de cambio y devolución.
- Fotos de producto: existen, con qué calidad y consistencia (mismo fondo, misma luz). Es el
  activo número uno de una tienda.
- Qué conversión manda: compra directa, consulta por WhatsApp, pedido de presupuesto.

### Portfolio / galería
- Qué trabajos van, con qué piezas (imágenes, video, links), y cuál abre.
- Si busca trabajo, clientes o solo mostrar: cambia dónde va el contacto.

### Docs / blog
- Fuente de los contenidos (Markdown, CMS), estructura (guías, referencia, changelog) y búsqueda.

## Qué anotar y cómo

Cada respuesta va al brief **textual o casi**. Las inferencias tuyas van marcadas como tales
("inferido: audiencia móvil, por ser un local de barrio"). Lo que el usuario deja abierto se
anota como abierto y se decide después, con el motivo escrito; nunca se rellena con un default
silencioso.
