# Plantilla de `design/BRIEF.md`

Una carilla. Solo hechos confirmados, inferencias marcadas y decisiones abiertas nombradas. Si un
bloque se lee como un *mood* ("moderno, limpio, confiable"), no está decidido todavía. Omití
secciones vacías antes que rellenarlas con prosa genérica.

```markdown
# Brief de diseño — <nombre del proyecto>
Fecha: <aaaa-mm-dd> · Modo: <de cero | auditoría: review/restyle/redesign | sección/componente>
Tipo de producto: <landing | institucional | app web/dashboard | e-commerce | portfolio | docs>
Modo de la superficie: <persuadir | operar | leer | experiencia>  (ver tipos-de-producto.md)

## Sujeto
<Qué es, quién está detrás, dónde. Dos o tres líneas, sin adjetivos.>

## Audiencia en situación
<Quién llega, desde dónde, sabiendo qué, en qué dispositivo, con qué urgencia.>
Inferido: <lo que supusiste, marcado>

## La única acción
<Qué tiene que hacer el visitante. Verbo + objeto. Una sola.>
Objeción principal: <la duda que la frena>

## Argumento de la página
Una línea por sección, en orden. Afirmación → prueba. Sin afirmación no hay sección.
1. <Afirmación> — prueba: <qué la demuestra; si no hay prueba real, cómo se muestra sin inventar>
2. …

## Inventario del sujeto (8–12 cosas que solo tiene este cliente)
- nombre y qué significa / de dónde viene
- dirección, calle, barrio y cómo se ve (sus veredas, su luz, sus carteles)
- números reales (años, mesas, metros, cuadras al río, precio, horario)
- la restricción con la que vive (solo por encargo, cierra en invierno, un turno por día)
- materiales y colores propios
- rituales y horarios
- cosas impresas de su mundo (un ticket, una etiqueta, un menú, un cartel)
- …
→ La idea de la página sale de acá, no de la categoría. Test del competidor: si la idea sirve para
el de la otra cuadra, no es una idea.

## Material real disponible
Fotos propias: <sí/no, cuántas, de qué, calidad> · Producto: <…> · UI real: <…> · Logo: <formato>
· Video: <…> · Textos existentes: <…>
Lo que NO hay y no se va a fingir: <…>
Plan de imágenes: <propias / generadas / archivos abiertos con crédito / dibujadas en código>

## Fijos (no se discuten)
Marca: <colores, fuentes, logo impuestos>  ·  Stack: <detectado | elegido | delegado: …>
Deploy: <…>  ·  Plataforma/CMS: <…>  ·  Debe sobrevivir (auditoría): <rutas, formularios, datos, SEO>
Pedidos explícitos del usuario: <textual>

## Referencias
<URL> — vale adoptar: <patrones> · no se copia: <activos>
…
En común: <tres rasgos>  ·  Contraejemplos (lo que no quiere): <…>

## Dirección (se completa en el paso 5)
Repartida: <nombre, seed> · elegida porque: <una línea> · redraws: <slot — motivo>
Idea: "En esta página, **<algo del sujeto>** se convierte en **<el dispositivo que pide la dirección>**."
Live thing: <la única cosa que el visitante puede hacer o que cambia con cada visita>
Estrategia de color: <contenida | comprometida | paleta completa | empapada> · claro/oscuro porque: <escena de uso>
Tipografía: <una o dos familias, y por qué estas>

## Abierto
- <decisiones pendientes y quién las toma>

## Contenido de muestra a confirmar antes de publicar
- <…>
```

## Mapeo a `PRODUCT.md` (si impeccable está instalada)

impeccable guarda la "verdad del producto" en `PRODUCT.md` y la lee en todos sus comandos. No
dupliques a mano si podés correr `/impeccable init`; si lo escribís vos, respetá su esquema:

| Brief | PRODUCT.md |
|---|---|
| Sujeto + Audiencia | `## Users`, `## Product Purpose` |
| Inventario (lo que solo tiene este) | `## Positioning`, `## Operating Context` |
| Fijos: stack, plataforma, debe sobrevivir | `## Platform` (`web`), `## Stack`, `## Capabilities and Constraints` |
| Fijos: marca | `## Brand Commitments` |
| Material real / lo que no hay | `## Evidence on Hand` (incluye las ausencias que no se inventan) |
| Accesibilidad requerida | `## Accessibility & Inclusion` |

Lo visual (dirección, paleta, tipografía, idea) **no** va a `PRODUCT.md`: impeccable lo espera en
`DESIGN.md` al final de la construcción, y taste-skill lo guarda en `.taste-skill/`. En el brief
queda la copia legible para el usuario.
