# Recetas: qué skill, en qué orden, según el caso

Si no sabés por dónde empezar, usá la **fórmula por defecto**. Si sabés qué tenés entre manos,
buscá tu caso abajo. En todas, lo que escribís en Claude Code va entre comillas; el resto lo hace
design-director solo (detecta las skills, pregunta, escribe el brief y llama a cada una en su
momento). No hace falta invocar las skills a mano salvo que quieras forzar una.

## Las cinco, en una línea cada una

| Skill | Es | Entra en |
|---|---|---|
| **design-director** (esta) | el director: entrevista, brief, referencias, orquesta | siempre, primero |
| **impeccable** | la verdad del producto al principio y la QA técnica al final | `init` al inicio · `audit`/`polish`/`harden` al cierre · `typeset`/`colorize`/`layout` en rediseños |
| **ui-ux-pro-max** | el mapa del rubro: patrón, anti-patrones, paleta y tipografía razonables, guías UX por stack | después de `init`, antes de diseñar; y consultas puntuales mientras construís |
| **taste-skill** | el director de arte: la idea del sujeto, tres direcciones, fotos reales, inspector en Chrome, crítica de jurado | en el centro: desde la dirección hasta el gate |
| **emilkowalski/skills** | el design engineer: qué animar y qué no, easing, duración, que la app se sienta nativa, romper la UI con datos feos | después de construir, antes del cierre |
| **gsap-skills / Motion AI Kit** (opcionales) | la API de la librería de animación | solo cuando Emil o taste-skill ya decidieron qué animar |

Regla de oro para combinarlas: **cada una toca un momento distinto, no el mismo**. Si dos
corren sobre el mismo paso, se pelean. Si ninguna corre en un paso, el paso sale genérico.

---

## La fórmula por defecto (cuando no sabés qué hacer)

Sirve para el 80 % de los casos: una landing, un sitio, una página de producto.

```
 1. "quiero diseñar <lo que sea>"          → design-director arranca: modo, entrevista, brief
 2. /impeccable init                        → PRODUCT.md (responde con el brief, no repitas)
 3. ui-ux-pro-max --design-system           → design/base.md: patrón del rubro + anti-patrones
 4. taste-skill                             → inventario → argumento → 3 direcciones → idea → copy deck
 5. construir                               → tokens → hero → secciones → fotos reales → móvil
 6. lint.mjs + inspect.mjs (0 FAIL)         → el gate de taste-skill a 1440/768/390
 7. crítica sobre capturas × hasta 3        → 14 pasadas + score; arreglar los 3 peores; repetir
 8. motion: find-animation-opportunities    → animate → review-animations   (Emil)
 9. /impeccable audit → polish → harden     → cierre técnico
10. informe                                 → dirección, idea, créditos de fotos, qué queda abierto
```

Lo que escribís vos, en orden:

1. `"quiero diseñar una landing para <sujeto>. Tengo estas fotos en /fotos y me gustan estos
   sitios: <urls>"` (las URLs son opcionales).
2. Respondés la entrevista (tres rondas máximo).
3. `"ok"` al brief.
4. Elegís una de las tres direcciones cuando te las muestre (o decís `"elegí vos y anotá por qué"`).
5. Esperás. Cuando te muestre capturas, mirás y decís qué te molesta en lenguaje llano ("está todo
   a la izquierda", "el título es muy largo"): esas frases son las que mejor corrige.
6. `"ok, cerrá"` cuando te guste.

Costo aproximado: 30–45 minutos y bastantes tokens (taste-skill es cara). Si no tenés eso, mirá
"poco tiempo" abajo.

---

## Recetas por situación

### A. Landing o sitio de cero
La fórmula por defecto, tal cual. Si es un sitio de varias páginas, el run de taste-skill es para
la home; las interiores heredan los tokens y pasan por el gate y `impeccable audit`.

### B. App web, dashboard o backoffice de cero
```
design-director (modo: de cero, tipo: app web)
→ /impeccable init
→ ui-ux-pro-max --design-system  (query "<rubro> dashboard internal", --density 7-8)
   + --domain ux / --stack <shadcn|react|vue…> para formularios, tablas, estados
→ taste-skill en modo app:  draw.mjs --app --kind <kind>   (NO el run de páginas)
→ construir pantalla por pantalla (cada una responde una pregunta; estados vacío/cargando/error)
→ inspect.mjs --app
→ Emil: find-animation-opportunities → animate (regla de frecuencia) → mobile-native si se usa en el celular
→ break-ui en todo componente con datos del usuario
→ /impeccable audit → harden → polish
```
Si el proyecto ya tiene shadcn/MUI/Vuetify: se heredan, taste-skill solo pone tokens y criterio.

### C. E-commerce
Primero: ¿plataforma (Tienda Nube, Shopify, Woo) o propio?
- **Plataforma**: design-director + ui-ux-pro-max (`"fashion ecommerce small brand"`) +
  taste-skill para la home y la ficha de producto → se diseña el **tema**, no el checkout.
  `tipos-de-producto.md` § e-commerce para PLP/PDP/carrito. Cierre con `impeccable audit`.
- **Propio**: la fórmula por defecto para home/PDP (Persuadir) y la receta B para carrito y
  checkout (Operar). `break-ui` en el carrito es obligatorio (nombres largos, 99 unidades,
  cupón inválido).
Y antes que cualquier skill: fotos de producto consistentes. Sin eso no hay receta que alcance.

### D. Auditar algo que ya existe (solo informe)
```
"auditame el diseño de <url o cómo levantarlo>"
→ design-director (modo: auditoría, alcance: review)
→ inspect.mjs <url> --out design/antes  +  lint.mjs
→ /impeccable audit + /impeccable critique
→ improve-animations   (si tiene motion; read-only)
→ design/AUDITORIA.md: puntaje técnico /20, crítica con score, tells, top 3, plan
```
Veinte minutos, pocos tokens, nada se toca. Es el mejor primer paso para un cliente nuevo.

### E. Rediseñar algo que ya existe (restyle o redesign)
La receta D primero, siempre. Después:
```
→ ui-ux-pro-max --design-system  (--keep de lo que la marca fije)
→ restyle:  /impeccable typeset → colorize → layout → harden → adapt
            motion: remove-animations (si está sobreanimada) → plan de improve-animations → review-animations
   redesign: taste-skill desde "argumento" con el contenido real, misma stack
→ inspect.mjs --out design/despues  →  comparar antes/después, clickear todo lo que andaba
→ /impeccable audit (de nuevo) → polish → informe con medidas lado a lado
```
Nunca se migra de framework ni de librería de estilos en un rediseño.

### F. Una sección o un componente
```
"rehacé el hero / armá un checkout / una tabla de pedidos"
→ design-director (modo 3): hereda tokens y composición; sin dirección nueva
→ prototype (Emil) si querés comparar 2-3 variantes en vivo
→ construir → gate sobre la página que lo contiene → crítica de la captura
→ animate + review-animations si tiene movimiento → break-ui si muestra datos
```
No corras `init`, `--design-system` ni `draw.mjs` para un componente.

### G. "Solo quiero que las animaciones estén bien"
No hace falta design-director. Directo con Emil:
```
find-animation-opportunities  → qué sí y qué no (read-only)
animate                       → cada pieza
review-animations             → el diff
animation-performance         → si algo tartamudea
remove-animations             → si "se siente lenta" o "hay demasiada animación"
```
GSAP o Motion solo para escribir la API de una pieza que Emil ya decidió.

### H. "Funciona en Chrome pero en el celular se siente raro"
`mobile-native` (Emil) primero: hover pegajoso, flash de tap, 100vh, inputs que hacen zoom,
notch, carruseles. Después `/impeccable adapt` si el móvil es el desktop apretado. Después
`inspect.mjs` a 390.

### I. Poco tiempo o pocos tokens
Versión corta que igual evita el slop:
```
design-director (entrevista de una ronda, brief corto)
→ ui-ux-pro-max --design-system           (segundos)
→ dirección a mano: 7 opciones del mundo del sujeto, dado, elegir una (orquestacion.md § 3, sin taste-skill)
→ construir con las reglas de la casa
→ Playwright a 1440/390 + gate manual de auditoria.md § 5
→ /impeccable audit
```
Lo que perdés: las fotos de archivos abiertos, el inspector automático y la crítica de jurado.
Lo que no perdés: la idea del sujeto y las prohibiciones.

### J. Tengo referencias y quiero que las use bien
Pasalas desde el primer mensaje. design-director las captura con `inspect.mjs <url>` (medidas
reales: fuentes, tamaños, colores), llena una ficha por sitio, saca lo común y te lo devuelve en
cinco líneas para confirmar. Eso pesa en la elección de dirección de taste-skill. No se copia
ninguna; se adoptan patrones.

---

## Qué no hacer

- No correr `draw.mjs` (taste-skill) y `--design-system` (ui-ux-pro-max) **después** de haber
  decidido: solo van a contradecir lo decidido. Van antes.
- No correr `impeccable audit` sobre un esqueleto: audita al final.
- No usar el run de páginas de taste-skill para una pantalla de app (`--app` existe para eso).
- No animar con GSAP/Motion antes de que Emil o taste-skill digan qué se anima.
- No mezclar dos librerías de animación en una página.
- No pedir "colores" ni "estilo" en la entrevista: salen del sujeto y de las referencias.
- No inventar prueba (reseñas, logos, cifras) para llenar una sección.

## Si todo lo demás falla

`"usá la skill design-director y arrancá por la fórmula por defecto"`. Te va a preguntar lo mínimo
y va a elegir por vos lo que no respondas, dejando escrito por qué.
