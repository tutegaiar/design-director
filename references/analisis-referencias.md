# Análisis de páginas modelo

Cuando alguien dice "me gusta este sitio", casi nunca sabe decir *qué* le gusta. El trabajo acá es
nombrarlo: medir y mirar dos a cuatro sitios, encontrar lo que tienen en común, separar los
**patrones** (que se adoptan) de los **activos** (que son de ellos y no se tocan), y devolverle al
usuario una lectura de su gusto que pueda confirmar.

Dos límites que no se negocian:

- **Se extraen patrones, no se clona.** Composición, proporciones, jerarquía, ritmo, tipo de
  imágenes, dispositivos de conversión: sí. Su paleta exacta, su tipografía si es una licencia o
  parte de su identidad, su logo, sus fotos, sus frases, sus ilustraciones: no. Si después del
  trabajo alguien puede decir "esto es una copia de X", falló.
- **La referencia informa la dirección, no la reemplaza.** La idea de la página sigue saliendo del
  sujeto del usuario (su calle, su nombre, su material). Una composición prestada con una idea de
  categoría da una página correcta y olvidable.

## 1. Capturar

Por cada URL, en este orden de preferencia:

1. **taste-skill instalada**: `node <taste>/scripts/inspect.mjs <url> --out design/refs/<slug>`.
   Te deja capturas a 1440/768/390 (fold y página entera por tramos) y **medidas reales**: fuentes
   efectivamente cargadas, tamaño del titular y del cuerpo, ratio entre ambos, colores dominantes,
   cantidad de reglas/sombras/gradientes, márgenes. Las medidas son oro: después podés pedirle a
   tu propia página las mismas proporciones.
2. **Playwright** (`npx playwright screenshot --viewport-size=1440,900 --full-page <url> out.png`
   y lo mismo a 390), o Chrome DevTools MCP / claude-in-chrome si están conectados.
3. **Sin navegador**: `WebFetch` del HTML y la CSS principal. Leés `font-family`, `@font-face`,
   variables de color, `max-width` del contenedor, estructura de secciones. Es peor, porque no ves
   la composición; decilo en el informe.

Si el usuario pasó **capturas en vez de URLs**, se analizan igual (abrilas con la herramienta de
lectura de imágenes); no vas a tener medidas, estimalas y marcalas como estimadas.

Abrí cada captura antes de escribir una palabra. Se juzgan las imágenes, no el código.

## 2. La ficha por sitio

Una por referencia, en `design/referencias.md`. Corta: lo que no se puede llenar en una línea no
va.

```markdown
## <nombre> — <url>
Qué es: <tipo de producto y rubro>  ·  Modo: persuadir / operar / leer / experiencia

**Un segundo**: <qué se ve primero: una palabra, una foto, un objeto, "un sitio web">
**Cinco segundos**: <se entiende qué es, para quién y qué hacer? sí/no, por qué>
**Idea**: <la que se puede decir en una frase, si la hay; o "ninguna más allá del formato">

**Estructura** (una palabra por sección, en orden): hero-foto-plena · split · lista · statement ·
grilla · full-bleed · índice · cierre-con-nombre …
**Tipografía**: <familias cargadas> · titular ~<px> / cuerpo ~<px> · ratio ~<n> ·
alineación · cuántos tamaños visibles · tracking apretado o no
**Color**: <proporción: qué color ocupa el ground, cuál la tinta, dónde aparece el acento y
cuántas veces> · claro/oscuro · campos de color por sección sí/no
**Imágenes**: <cuántas, de qué tipo (foto propia, producto, archivo, ilustración, UI real),
qué tamaño ocupa la del hero, recortes consistentes sí/no, hay video>
**Espacio y marco**: márgenes <px> iguales sí/no · separación entre secciones ~<px> ·
densidad baja/media/alta · bordes de texto alineados (cuántas x distintas)
**Componentes**: nav <qué tiene> · botones <forma, cantidad en el hero> · footer <sitemap o cierre>
**Movimiento**: <una pieza firmada / entradas por sección / nada / exceso>
**Conversión**: <dónde está el CTA, cuántas veces, qué prueba usa y de qué tipo, qué objeción
responde>
**Tells de IA presentes**: <eyebrows, 01/02/03, cards con ícono, gradiente, glass… o "ninguno">

**Vale adoptar**: <2–4 patrones concretos>
**Es de ellos, no se copia**: <paleta exacta, fuente firma, foto, frase, ilustración>
```

## 3. Lo que tienen en común

Después de las fichas, una sección `## En común` con lo que se repite en dos o más referencias.
Acá está el gusto del usuario. Buscá en estos ejes:

| Eje | Preguntá | Traducilo a |
|---|---|---|
| Escala tipográfica | ¿Titulares enormes (ratio > 5) o moderados (~3)? | el ratio objetivo de tu página |
| Cantidad de color | ¿Un acento sobre neutro, un color que ocupa la mitad, o la página *es* el color? | estrategia: contenida / comprometida / paleta / empapada |
| Claro u oscuro | ¿Y en qué escena de uso lo justifica? | ground |
| Densidad | ¿Mucho aire o mucho contenido por pantalla? | separación entre secciones y tamaño de cuerpo |
| Imágenes | ¿Foto grande dominante, muchas chicas, ilustración, UI real, nada? | el piso de imágenes y el tipo de búsqueda en archivos |
| Composición | ¿Centrado y simétrico, o asimétrico con grilla visible? | la familia de direcciones a elegir en `draw.mjs` |
| Movimiento | ¿Una pieza firmada o quietud? | el presupuesto de motion |
| Tono de copy | ¿Corto y seco, cálido, técnico? | el copy deck |
| Conversión | ¿CTA único arriba, o repetido, o diferido tras la prueba? | el argumento de la página |

Si las referencias se contradicen entre sí (una densa y oscura, otra aireada y clara), decíselo al
usuario y preguntá cuál de las dos lecturas pesa más. No promedies: el promedio de dos
direcciones es la página genérica que esta skill existe para evitar.

## 4. Lo que no se adopta aunque esté

Las referencias que el usuario elige suelen traer tells que *a él le gustan* porque los vio mil
veces. Nombralos en la ficha y, si el usuario insiste en uno, se respeta como **fijo** y se anota
en el brief para que el inspector no lo marque (`--allow` en taste-skill). Pero por defecto, que
una referencia use eyebrows o cards con ícono no es motivo para usarlas.

Tampoco se adopta lo que depende de un activo que el usuario no tiene: una referencia con
fotografía de producto impecable no sirve de modelo de composición para una tienda sin fotos. En
ese caso el patrón que se extrae es "la foto manda", y la consecuencia es conseguir las fotos o
cambiar de composición, no simular la foto.

## 5. Devolución al usuario

Cinco líneas, antes de seguir:

1. "Lo que tus referencias tienen en común es…" (tres rasgos, en lenguaje llano).
2. "De cada una vale tomar…" (un patrón por sitio).
3. "No voy a copiar…" (lo que es de ellos).
4. "Donde se contradicen, entiendo que preferís…" (si aplica).
5. "¿Leí bien?"

Con el OK, los patrones adoptados pasan al brief (sección *Referencias*) y pesan en la elección de
dirección: si taste-skill reparte tres direcciones, elegís la que mejor carga el patrón común
**y** algo que solo tiene este sujeto; si ninguna lo hace y podés decir por qué, es un `--redraw`
con motivo escrito.
