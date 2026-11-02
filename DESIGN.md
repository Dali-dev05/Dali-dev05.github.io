# DESIGN.md

**Dali Muñoz Moreno · Personal CV & Projects**
Mode: **Persuade** · Platform: **web** · Build: **code-led**

Derived from **Vercel's** design language (`vercel.com`), filtered through [Impeccable's craft floor](reference/craft-floor.md). The brief: a personal page whose entire purpose is to put the author's work, skills, and credentials in front of recruiters and collaborators in seconds.

> The craft floor holds mechanics, never direction. The palette, type, and materials below are the committed world; the craft-floor clauses below are the non-negotiables.

---

## 1. Direction contract

| Block | Commitment |
|---|---|
| **Thesis** | A personal page that makes the author's real work, skills, and credentials legible in seconds — not a generic template dashboard. |
| **Own-world** | Clean, modern, confident: near-white canvas, near-black ink, one indigo/violet accent, Inter as display **and** body, generous whitespace, flattened depth, one authored entrance. |
| **Story** | A visitor understands: Dali Muñoz Moreno is a practical full-stack developer whose work is readable at a glance. Recruiters land on a CV, scan real projects, and find the contact. |
| **First viewport** | Display-led hero: large, confident heading; one job-like subtext; one primary call-to-action. Nothing above the fold competes with the author's name. |
| **Form** | form: new-world / vercel-inspired · seed: none (unavailable) |
| **Finish** | unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance. |

---

## 2. Design principles

1. **Legibility is the primary affordance.** A recruiter finds the work, the skills, and the contact in seconds.
2. **Content at 20 paces.** Visuals are subtle; the content is loud.
3. **No floating boxes.** Depth comes only from soft, real shadows, and only where it clarifies state or hierarchy.
4. **One motion moment.** One authored entrance; everything else stays still.
5. **Tokens, not one-off values.** Every spacing, color, and type step is a variable.
6. **Built, not assembled.** No browser-default chrome masquerading as design; real scrollbars, focus rings, underlines, and numerals.

---

## 3. Color system

**OKLCH tokens** (per impeccable's colorizing guidance; grounded in Vercel's near-white / near-black / indigo core):

| Role | CSS variable | OKLCH | Hex | Where it lives |
|---|---|---|---|---|
| **canvas** | `--c-canvas` | `oklch(0.985 0 0)` | `#fafafa` | Page ground |
| **surface** | `--c-surface` | `oklch(1 0 0)` | `#ffffff` | Elevated cards, hero panels |
| **surface-elevated** | `--c-surfaceElev` | `oklch(0.975 0.012 260)` | `#f0f0ff` | Raised panels, nav, subtle tint |
| **ink** | `--c-ink` | `oklch(0.11 0 0)` | `#121212` | Primary copy |
| **ink-secondary** | `--c-inkSecondary` | `oklch(0.38 0 0)` | `#575757` | Descriptions |
| **ink-tertiary** | `--c-inkTertiary` | `oklch(0.45 0 0)` | `#737373` | Captions, meta |
| **border** | `--c-border` | `oklch(0.92 0 0)` | `#e4e4e7` | Dividers, card edges |
| **border-focus** | `--c-borderFocus` | `oklch(0.62 0.17 265)` | `#6366f1` | Focus rings |
| **accent** | `--c-accent` | `oklch(0.66 0.17 265)` | `#6366f1` | Primary action, active nav link |
| **accent-hover** | `--c-accentHover` | `oklch(0.60 0.16 270)` | `#4f46e5` | Button hover, active link |
| **accent-soft** | `--c-accentSoft` | `oklch(0.93 0.07 260)` | `#e0e7ff` | Filled accent background |
| **good** | `--c-good` | `oklch(0.49 0.16 145)` | `#16a34a` | Success states |
| **error** | `--c-error` | `oklch(0.56 0.2 25)` | `#dc2626` | Errors, destructive |

**Rules**

- Strongest color owns one deliberate region or role. Never scatter tiny accents.
- On colored surfaces, tint secondary text from the foreground or surface hue — never a washed-out generic gray.
- The primary action is the only place the accent owns a large area.
- No color conveys state alone: pair color with text, icon, or position.

---

## 4. Typography

**Family:** Inter — a single, deliberate family for display and body. Self-hosted via `@font-face` (never a hosted stylesheet). Fallbacks: system-ui, -apple-system, sans-serif.

**Type ramp** (measured at 16px root; body measure 65–75ch, headings tight and weight-driven):

| Role | CSS variable | Size | Weight | Line-height | Measure |
|---|---|---|---|---|---|
| `display` | `--t-display` | `clamp(2.6rem, 5vw, 4.2rem)` | 700 | 1.15 | 40–55ch |
| `h1` | `--t-h1` | `2.25rem` | 700 | 1.2 | 50–65ch |
| `h2` | `--t-h2` | `1.75rem` | 600 | 1.3 | 55–70ch |
| `h3` | `--t-h3` | `1.25rem` | 600 | 1.35 | 60–75ch |
| `body` | `--t-body` | `1rem` | 400 | 1.65 | 65–75ch |
| `label` | `--t-label` | `0.875rem` | 600 | 1.5 | — |

Rules
- `text-wrap: balance` on headings and short centered blocks; `text-wrap: pretty` on body.
- Hard breaks only between phrases; a heading that lands on one word for weight is a hard-break and must be deliberate.
- Zoom and text scaling stay intact; do not lock with fixed px unless intentional.

---

## 5. Layout & spacing

**Reading path.** Primary (the name and the job), then the scanable list of projects, then the CV detail, then the contact. This path is linear and stable.

**Spacing.** 4-unit base scale: `4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96px`. Generous above a heading, tighter between siblings. `gap` for sibling rhythm.

**Topology**

- **Top bar** (sticky): name mark + nav; thin divider; collapses to a numbered menu on narrow.
- **Hero** (first viewport): author name, one-line job, the CTA. Nothing else above the fold.
- **Body**: a single vertical rhythm. CV summary → skills → projects → contact.
- **Projects** are a responsive grid (2 → 1 columns) driven by content, not a fixed card carousel.
- **Contact** is a short, actionable close: email with a copy target, a GitHub link, and the page itself.

**Responsive behavior**

- < 640px: stack everything, widen type blocks, drop secondary nav into a compact menu.
- 640–1024px: rebalance the projects grid to 2 columns where it helps.
- > 1024px: restore the full 2–3 column layout.

---

## 6. Components

### 6.1 Button

- **Primary**: accent background (`--c-accentSoft`) + accent text (`--c-accent`), `40px` height, `6px` radius, focused by `--c-borderFocus`.
- **Ghost**: subtle border, transparent bg, `--c-inkSecondary` text; hover to `--c-inkSecondary` text on `--c-surface`.
- States: `:hover`, `:focus-visible` (2px offset ring from `--c-borderFocus`), `:active`, `:disabled`.

### 6.2 Navigation

- Sticky at the top, `transparent` foreground, `1px` top border (`--c-border`).
- On scroll, surfaces to `--c-surfaceElev` with a soft bottom shadow.
- Logo (author initials) + anchored links; on narrow, a compact numbered menu.
- Focus rings follow `--c-borderFocus`.

### 6.3 Hero

- Display/type rank at the first viewport; author's name sits above the line, job subtitle, then one primary CTA.
- No eyebrow label above the heading (per craft floor — the heading carries its own weight).
- Subtle, soft shadow under the hero card; no hard-offset shadows.

### 6.4 Cards

- Border (`--c-border`), soft level-1 shadow, `10px` radius.
- One accent on the whole card (e.g., the project's tag color) — never per-cell.
- No icon tiles; text or a short inline icon carries the label.

### 6.5 Footer

- Thin, low-contrast, `lang` declared, links with real intent.

---

## 7. Motion

**One authored entrance** only, on the first viewport:

- The hero name fades in + translates `0 12px 32px` with the accent-soft backdrop, `400ms`, `cubic-bezier(0.22,1,0.36,1)`.
- Everything else stays still unless the user interacts.

**Motion rules**

- Respect `prefers-reduced-motion: reduce` — hand-hold the user.
- One authored element, one cadence. No scattered hover thrills.
- Blur, backdrop-filter, and clip-path belong to the palette when they stay smooth — and they always stay smooth here.

---

## 8. Accessibility & inclusion

- **Contrast** (WCAG AA): body ≥ 4.5:1, large text ≥ 3:1, controls/icons/focus ≥ 3:1. Checked per pair, not by eye.
- **Keyboard:** every interactive state reachable and clear; focus ring follows `--c-borderFocus`.
- **Semantics:** correct landmarks, headings, labels, `lang="es"`, `alt` on meaningful images.
- **States:** hover, focus, disabled, empty, error, and loading all carry non-color information.
- **Font scaling & zoom:** does not break the rhythm; `text-wrap: balance` is progressive.

---

## 9. Testing gates

- The squint test: primary, secondary, and major groups still read in order when detail is blurred.
- The first-viewport test: a first-time visitor knows what this is, why it matters, and what to do within seconds.
- The detector runs clean: `impeccable detect --json` reports no mechanical findings on the changed targets.
- The finish reviewer's verdict is recorded before the session ends.
