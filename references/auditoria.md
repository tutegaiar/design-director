# Auditoría y crítica

Dos cosas distintas que se confunden: la **auditoría técnica** mide lo verificable en el código y en
el render (contraste, foco, overflow, tokens, performance); la **crítica** juzga si la página es
buena. Una página puede pasar la auditoría y seguir siendo anónima. Las dos van en el informe.

Se critica sobre **capturas**, nunca sobre el código: el código lo escribiste vos y vas a leer tus
intenciones en él. La imagen solo muestra lo que hay.

## 1. Registrar el antes (modo 2) / el estado (paso 7)

```bash
node <taste>/scripts/inspect.mjs <url> --out design/antes        # o --out design/ronda-N
node <taste>/scripts/lint.mjs <fuentes>
/impeccable audit <target>
/impeccable critique <target>
```

Sin herramientas: Playwright a 1440×900, 768×1024 y 390×844 (fold y página completa), y el gate
manual de § 5.

Y leer el código: framework, método de estilos (Tailwind v3/v4, CSS modules, styled-components,
CSS plano, un tema de WordPress/Tienda Nube), componentes, dependencias, qué rutas/formularios/
datos/tracking tienen que sobrevivir.

## 2. Rúbrica técnica (0–4 por dimensión, 20 en total)

Adaptada del `audit` de impeccable; sirve con o sin él.

| # | Dimensión | Qué mirar | 0 | 2 | 4 |
|---|---|---|---|---|---|
| 1 | **Accesibilidad** | contraste ≥ 4.5:1 (3:1 texto grande); foco visible y orden lógico; sin trampas de teclado; headings jerárquicos y landmarks; botones que son `<button>`; `alt`; labels en inputs; errores asociados; `prefers-reduced-motion` con alternativa que conserva el cambio de estado (no un kill global a 0.01 ms) | falla WCAG A | esfuerzo parcial, huecos grandes | AA completo, roza AAA |
| 2 | **Performance** | imágenes en WebP/AVIF con lazy y espacio reservado (CLS < 0.1); animaciones solo de transform/opacity; sin blur/filtros sin límite; `will-change` solo donde hace falta; sin re-renders innecesarios; peso del bundle | layout thrash, todo sin optimizar | algo optimizado | rápido y liviano |
| 3 | **Theming** | colores por tokens, no hex sueltos; modo oscuro si existe con contraste correcto; tokens consistentes; cambio de tema sin valores que no se actualizan | todo hardcodeado | tokens inconsistentes | sistema completo |
| 4 | **Responsive** | sin anchos fijos que rompan; targets ≥ 44 px (mínimo legal 24 px con espaciado); sin scroll horizontal; texto que escala; móvil que es una composición propia; gestos táctiles que funcionan (sliders, drags) | solo desktop | anda en móvil con asperezas | fluido en todos los anchos |
| 5 | **Integridad de implementación** | atajos repetidos, deriva del sistema, contenido decorativo o engañoso (métricas falsas, logos inventados, placeholders que parecen datos), estructura intercambiable con otro producto | deriva sistémica | varios problemas verificados | coherente e intencional |

Bandas: 18–20 excelente · 14–17 bien · 10–13 aceptable · 6–9 pobre · 0–5 crítico.

## 3. Crítica: las catorce pasadas

Sobre `desktop-fold`, después las hojas de desktop, después `mobile-fold` y las de móvil. Una
pasada por vez, sin mezclarlas. (De `critique.md` de taste-skill; úsala con o sin ella.)

1. **Un segundo, después cinco.** Mirá y apartá la vista. ¿Qué viste? Tiene que haber una sola
   respuesta: una palabra, una imagen, un objeto. Si la respuesta es "un sitio web", no hay foco.
   Después cinco segundos como un extraño: ¿sabés qué es, para quién y qué hacer? Si el título
   solo se entiende después de scrollear, no es un título.
2. **Entrecerrar los ojos.** El texto se vuelve barras grises. La página tiene que reducirse a dos
   o tres masas grandes con diferencias claras. Muchas masas chicas iguales = todo es mediano,
   nada lidera.
3. **Tapar el logo.** ¿Esta primera pantalla podría ser de un competidor, o de otro rubro? Si
   cambiando el nombre y el sustantivo del titular la página sigue valiendo, no tiene idea. Y
   después scrolleá: ¿la idea llega a pricing, FAQ y footer, o la página se vuelve bloques de
   stock después de la primera pantalla?
4. **Bordes.** Seguí el borde izquierdo de cada bloque de texto. Contá las x distintas. Una página
   compuesta tiene dos o tres, reutilizadas a propósito. Seis significa que se colocaron las cosas
   de a una.
5. **Espacio y marco.** ¿Lo relacionado está cerca y lo no relacionado lejos? ¿El hueco entre
   secciones es claramente mayor que cualquier hueco interno? ¿Algún vacío es un agujero (por
   accidente) y no un descanso (por decisión)? ¿Los márgenes izquierdo y derecho son iguales?
   ¿Alguna sección tiene el texto en una mitad y la otra mitad vacía? ¿Hay un tramo de nada de
   más de media pantalla? Esto es lo primero que nombra un lector ("está todo a la izquierda",
   "espacio vacío al azar").
6. **Tipo.** ¿El salto de cuerpo a titular es decisivo (3× o más)? ¿Hay más de cinco tamaños?
   ¿Algún titular con una palabra huérfana en la última línea? ¿Algún párrafo de más de ~75
   caracteres o centrado en más de tres líneas?
7. **Color.** Nombrá las proporciones: qué color ocupa más superficie, cuál apoya, dónde está el
   acento. Un acento en diez lugares no significa nada. En la única acción y un detalle,
   significa "acá".
8. **Imágenes.** ¿Hay al menos cuatro reales, y una que se mueve? ¿Cada una hace un trabajo
   (muestra la cosa, sitúa el lugar, prueba la afirmación)? ¿Comparten recorte y grado? ¿Hay algún
   gris, alguna foto estirada, alguna pantalla falsa de barras?
9. **Igualdad.** Una palabra por la composición de cada sección (split, lista, full-bleed, grilla,
   statement, índice…). La misma palabra dos veces seguidas, o tres en la página, es la plantilla
   asomando.
10. **Teléfono.** ¿La pantalla de móvil es una composición propia, con su recorte y sus cortes de
    línea, o el desktop apretado? ¿La primera pantalla sigue siendo una sola cosa clara?
11. **Plenitud.** Pantalla por pantalla de desktop: ¿cada una es un póster compuesto, o una
    columna angosta de texto chico con tierra muerta a los lados? Una página austera no es una
    página contenida: si se puede confundir con un wireframe sin terminar, está subconstruida.
12. **Sustancia.** ¿Cada sección que pidió el brief entrega su información completa y legible (la
    carta entera, cada habitación, cada orador, el precio y qué incluye)? ¿El visitante se iría
    sabiendo lo que vino a averiguar? ¿El botón principal es un botón real en la primera pantalla?
13. **Colisiones.** ¿Algo tapa un titular, un statement o un botón en alguna posición de scroll?
    ¿Algo se sale del borde del teléfono? Una fila que scrollea de costado en móvil se lee como
    cortada.
14. **El competidor y el live thing.** Poné el nombre del competidor más cercano en la página:
    ¿la idea sigue funcionando? ¿Cuál es la única cosa viva? Si cualquiera de las dos respuestas es
    floja, ese es el primer problema de la ronda, antes que cualquier detalle.

Nota de los tests ciegos de taste-skill: una página más rica llena de dispositivos de plantilla le
ganó siempre a una más limpia pero delgada. Las reglas sacan los dispositivos; las pasadas 11–13
son donde te asegurás de no haber perdido la sustancia con ellos.

## 4. El score

Como jurado de Awwwards: cuatro criterios de 1 a 10, ponderados **diseño 40 % · usabilidad 30 % ·
creatividad 20 % · contenido 10 %**.

- **Diseño** (composición, tipografía, color, imágenes, oficio): 9–10 cada pantalla aguanta como
  póster · 8 seguro y coherente, uno o dos puntos blandos · 7 limpio y profesional, poca tensión ·
  6 prolijo pero anónimo, parece un kit · ≤ 5 jerarquía débil, espaciado accidental, tipo default.
- **Usabilidad** (orientación en tres segundos, legible, acciones obvias, móvil honesto): 9–10
  sabés qué es, para quién y qué hacer sin scrollear, impecable en el teléfono · 8 claro, fricción
  menor · 7 funciona con un problema real · ≤ 6 hay que buscar o algo se rompe.
- **Creatividad** (una idea que se dice en una frase y se sostiene): 9–10 un concepto específico
  de este sujeto que no viste aplicado así · 8 idea clara con un movimiento memorable · 7
  ejecución con gusto de un enfoque conocido · ≤ 6 el default de la categoría.
- **Contenido** (palabras e imágenes específicas, verosímiles, editadas): 9–10 cada línea solo
  puede ser de este sujeto · 7–8 claro y concreto, algunas líneas genéricas · ≤ 6 slogans, relleno, stock.

`total = 0.4·diseño + 0.3·usabilidad + 0.2·creatividad + 0.1·contenido`

Calibración: un Site of the Day real queda en 7.5–8.0. Un 8.5 honesto es raro. Si tu primera nota a
tu propio trabajo es 9, puntualo de nuevo como el jurado que no lo construyó.

**Caps** (pisan la aritmética):
- cualquier FAIL del inspector todavía abierto → total ≤ **6.0**;
- un titular de tres o más líneas en algún ancho, un eyebrow, labels en mono, 01/02/03, un
  gradiente decorativo, una sombra en reposo o una hairline decorativa visible en captura → total
  ≤ **6.5**;
- falla la pasada 3 (podría ser de cualquiera) → creatividad ≤ **6**;
- la idea sirve para el competidor (pasada 14) → creatividad ≤ **7**.

## 5. Gate manual (sin `inspect.mjs`)

A 1440, 768 y 390, sobre el build de producción:

- [ ] un solo `h1`, con el título en la primera pantalla; un heading por sección
- [ ] ningún titular supera dos líneas
- [ ] márgenes exteriores iguales; ninguna sección con media pantalla vacía; ningún tramo vacío > media pantalla
- [ ] fuentes efectivamente cargadas son las decididas (DevTools → Network/Fonts); dos como máximo
- [ ] cuerpo ≥ 16 px en tinta plena; cinco tamaños como máximo
- [ ] cero gradientes, sombras en reposo, glows, blur, hairlines decorativas, eyebrows, mono fuera de código, 01/02/03, emoji-ícono, cards con ícono
- [ ] contraste de todo texto ≥ 4.5:1 (DevTools o `npx pa11y <url>`)
- [ ] foco visible en todo control; recorrido completo con Tab; nombre accesible en íconos
- [ ] sin scroll horizontal en 390; targets ≥ 44 px
- [ ] imágenes: ≥ 4 reales en páginas, con `alt`, en WebP/AVIF, lazy, con espacio reservado
- [ ] `prefers-reduced-motion` respetado; nada oculto si falla el script
- [ ] Lighthouse accesibilidad ≥ 95 y performance razonable (`npx lighthouse <url>`)

## 6. Formato del informe (`design/AUDITORIA.md`)

```markdown
# Auditoría — <proyecto> — <fecha>
Alcance: <páginas/pantallas> · Modo: <persuadir/operar/leer> · Stack: <…> · Herramientas: <inspect.mjs | impeccable audit | Playwright | manual>

## Resumen en tres líneas
<qué es, cómo está, qué pasaría si se arreglan las tres cosas de abajo>

## Puntaje técnico — <n>/20 (<banda>)
| # | Dimensión | Puntaje | Hallazgo clave |
|---|---|---|---|
| 1 | Accesibilidad | ? | … |
| 2 | Performance | ? | … |
| 3 | Theming | ? | … |
| 4 | Responsive | ? | … |
| 5 | Integridad | ? | … |

## Crítica — <total> (diseño ?, usabilidad ?, creatividad ?, contenido ?) · caps aplicados: <…>
<una línea por pasada que encontró algo, con la medida o la captura que lo prueba>

## Tells de página generada presentes
<lista, con dónde y con qué se reemplaza cada uno (ver anti-slop.md)>

## Las tres cosas que más mueven la aguja (impacto / riesgo)
1. <qué, por qué, cuánto cuesta, qué toca>
2. …
3. …

## Plan completo, en orden
tipografía → color → marco → estados → componentes genéricos → motion → técnica
<cada ítem con archivo/componente afectado y qué no se puede romper>

## Lo que funciona y se conserva
<…>

## Medidas (antes → después, si ya se intervino)
| Métrica | Antes | Después |
|---|---|---|
| titular 1440 / 390 (px, líneas) | | |
| cuerpo (px) · ratio | | |
| fuentes cargadas | | |
| FAIL / WARN inspector | | |
| contraste mínimo | | |
| Lighthouse a11y / perf | | |
| puntaje técnico / crítica | | |
```

## 7. Cuándo parar

Tres rondas de mirar→arreglar como máximo. Se para antes cuando: 0 FAIL en los tres anchos, las
pasadas 1, 3, 5, 11, 12 y 14 pasan, y la nota no sube más de 0.3 entre rondas. Lo que queda flojo
se dice en el informe; no se pule en silencio hasta el infinito.
