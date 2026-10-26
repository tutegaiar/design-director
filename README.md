# design-director

Skill de Claude Code que actúa como director/a de diseño web: entrevista antes de construir,
analiza páginas modelo (opcional), escribe un brief y recién después orquesta en el orden correcto
[taste-skill](https://github.com/Leonxlnx/taste-skill),
[ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) e
[impeccable](https://github.com/pbakaus/impeccable), degradando bien si alguna no está instalada.

Sirve para landings, sitios institucionales, apps web y dashboards, e-commerce, portfolios y docs,
en cualquier stack. Tiene dos modos principales: **proyecto de cero** y **auditoría / rediseño**
de algo existente, más un modo acotado para una sección o componente.

## Instalación

**Con el CLI de skills (recomendado):**

```bash
npx skills add https://github.com/tutegaiar/design-director
```

**A mano, global (todos tus proyectos):**

```bash
git clone https://github.com/tutegaiar/design-director ~/.claude/skills/design-director
```

**A mano, solo en un proyecto:**

```bash
git clone https://github.com/tutegaiar/design-director .claude/skills/design-director
```

Reiniciá la sesión de Claude Code después de instalarla.

## Skills hermanas (opcionales, pero es lo que la hace potente)

```bash
# taste-skill (Node 22+, Chrome/Edge/Chromium)
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"

# ui-ux-pro-max (Python 3)
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill

# impeccable
npx impeccable install
```

## Uso

En Claude Code, dentro de tu proyecto:

```
quiero una landing para una panadería de barrio
auditame el diseño de esta página: http://localhost:3000
rediseñá el checkout
```

La skill se activa sola con pedidos de diseño, rediseño, auditoría o "que se vea mejor". También
podés invocarla explícitamente: `usá la skill design-director`.

## Estructura

```
design-director/
├── SKILL.md                      flujo principal: detección, modo, entrevista, brief, ejecución
└── references/
    ├── entrevista.md             preguntas por modo y por tipo de producto
    ├── analisis-referencias.md   protocolo para analizar páginas modelo
    ├── brief-template.md         plantilla de design/BRIEF.md y mapeo a PRODUCT.md
    ├── orquestacion.md           orden de las tres skills, comandos, conflictos, degradación
    ├── tipos-de-producto.md      landing, institucional, app web, e-commerce, portfolio, docs
    ├── auditoria.md              rúbrica técnica, 14 pasadas de crítica, score, informe
    └── anti-slop.md              registro de tells de página generada y reemplazos
```

## Licencia

MIT
