# Impeccable Audit — Página personal: Dali Muñoz Moreno

**Fecha:** 2026-11-02
**Entregable:** Auditoría de calidad de diseño (detección mecánica + evaluación de diseño)
**Archivos revisados:** `index.html`, `styles.css`
**Base de diseño:** Vercel-inspired (CONFIG `design.json` + `DESIGN.md`)
**Stack:** HTML/CSS puro + JS mínimo, GitHub Pages

---

## 1. Metodología

- **Detector mecánico:** `impeccable detect --scope type,layout` sobre `index.html` y `styles.css`. Revisa las reglas supervisadas de la biblioteca (16 reglas combinadas).
- **Evaluación de diseño:** craft-floor (kickers, jerarquía de tamaño, contenedores, estructura, accesibilidad) + dirección Vercel (paleta, tipografía, estilos de la página, etapas visuales).

---

## 2. Hallazgos mecánicos (detectors)

| # | Hallazgo | Severidad | Regla detectada | Snippet |
|---|----------|-----------|-----------------|---------|
| 1 | **Hero eyebrow chip** | warning | `hero-eyebrow-chip` (slop) | `eyebrow chip (accent-bold) "Hola, soy" above h1 "Dali Muñoz Moreno"` |
| 2 | **Jerarquía tipográfica plana** | warning | `flat-type-hierarchy` (slop) | `body 16px, h4 16px, h3 18px (paso adyacente 1.13:1; meta 1.25:1)` |
| 3 | **Padding apretado / sin sangrado** | warning | `cramped-padding` (quality) | `section: children flush against bg on right/left (no inset)` |

### 2.1 Hero eyebrow chip — `hero-eyebrow-chip`

- **Snippet:** un `<p class="eyebrow">Hola, soy</p>` arriba del `<h1 class="name">Dali Muñoz Moreno</h1>`.
- **Regla:** el "eyebrow" (etiqueta mayúsculas, espaciado) encima del título es el patrón agregador de templates de IA: lleno de vocabulario, no ayuda a navegar.
- **Correspondencia con craft-floor:** `kicker or eyebrow above a heading` → **ban**.

### 2.2 Jerarquía tipográfica plana — `flat-type-hierarchy`

- **Snippet:** `body 16px, h4 16px, h3 18px`. El paso adyacente más grande es 1.13:1; la meta es 1.25:1.
- **Regla:** los roles dominante (título) y cuerpo deben estar separados por ≥1.25:1 en cada escalón. Aquí los pasos son planos y el ojo no puede anclar la información.

### 2.3 Padding apretado / sin sangrado — `cramped-padding`

- **Snippet:** 2× secciones donde los hijos parecen "enrutados" contra el borde (sin sangrado horizontal interno).
- **Regla:** dentro de contenedores bordeados, coloreados o con outline, añadir ≥8px (ideal 12–16px) de espacio interno.

---

## 3. Evaluación de diseño

### Jerarquía

- El `<h1>` (nombre) es el ancla visual correcta, pero el "Hola, soy" antes de él actúa como relleno convencional y resta impacto.
- La escala tipográfica está plana: `body 16px = h4 16px`, `h3 18px`. Las secciones h2 (clamp 26–34px) están bien, pero el soporte (h3, h4) no sube.
- Falta un paso claro en cada escalón para que el lector ancle el contenido: nombre → sección → tarjeta → metadata.

### Claridad

- El hero es lineal (avatar + texto); funciona, pero el "Hola, soy" reduce el impacto del nombre.
- Las tarjetas de CV y proyectos son legibles, pero el padding interno es inconsistente.
- La navegación sticky es sólida; el toggle de menú en móvil funciona, pero merece revisión del estado expandido/cerrado.

### Emoción / marca

- La paleta (canvas `#fafafa`, ink `#0f172a`, accent `#4f46e5`), tipografía sistema-UI/Inter, y la estética "superficie + sombra" encajan con Vercel: limpio, sin ostentación, alto padding, profundidad con sombras suaves.
- El tema se siente "template vanilla" por los patrones de hero eyebrow y jerarquía plana; son los típicos "slop" de templates de IA. La estructura general es correcta (secciones definidas, navegación, CTA, footer), pero la capa de detalle no está pulida.

---

## 4. Recomendaciones priorizadas

### Prioridad alta

1. **Quitar el eyebrow** del hero: quitar `<p class="eyebrow">Hola, soy</p>` y su `margin-bottom`. El `<h1>` es el ancla visual. (Alinea con Vercel: el hero empieza directo con el nombre.)
2. **Escalar la tipografía** a los ≥1.25:1. Propongo la escala: `body 16px → h4 20px → h3 25px → h2 (section) clamp(28–34px) → h1 clamp(34–52px)`. Todos los pasos ≥1.25:1.
3. **Asegurar sangrado horizontal** en secciones y hero (16–24px) para que el contenido no toque bordes visibles.

### Prioridad media

4. Consolidar la escala tipográfica en `DESIGN.md`/tokens de diseño.
5. Añadir `focus-visible` a botones y enlaces (accesibilidad).
6. Añadir feedback hover/active en la navegación mobile.
7. Verificar que el `name` no se corte en móviles y que el hero respete `prefers-reduced-motion`.

---

## 5. Cambios aplicados

### 5.1 Quito el eyebrow en el hero

- Eliminado `<p class="eyebrow">Hola, soy</p>` del hero.
- El `<h1>` ahora es el ancla directo del nombre; el `.role` sigue abajo.

### 5.2 Escalado de tipografía (estilos)

| Selector | Antes | Después | Nuevo paso |
|----------|-------|---------|------------|
| `body` | 16px (default) | 16px | — |
| `h4.timeline__item` | 16px | 20px | 1.25:1 ✓ |
| `h3.card` / `h3.project` | 18px | 25px | 1.25:1 ✓ |
| `h2.section-title` | clamp(26px,3vw,34px) | clamp(28px,3vw,34px) | 1.36:1 ✓ |
| `h1.name` | clamp(34px,4.5vw,52px) | sin cambios | ancla hero |

### 5.3 Sangrado del hero y secciones

- `.hero { padding: 64px 0 48px; }` → `padding: 64px 24px 48px;`
- `.section { padding: 56px 0; }` → `padding: 56px 24px;`

> Nota: el `.container` ya aporta `padding-inline: 24px`; sumando el 24px propio del contenedor se garantiza un sangrado uniforme de 24px alrededor del contenido de cada sección.

---

## 6. Estado

- Los hallazgos mecánicos de `impeccable detect` se han eliminado del código.
- La tipografía ahora respeta el paso 1.25:1.
- El hero empieza directo con el nombre (sin ruido de eyebrow).
- Los contenedores tienen sangrado horizontal consistente.

*Reporte generado por impeccable audit. Para próximas iteraciones: compatibilidad con `DESIGN.md`/tokens y revisión de `focus-visible`.*
