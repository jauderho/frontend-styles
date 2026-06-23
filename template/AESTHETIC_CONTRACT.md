# AESTHETIC_CONTRACT.md — "‹STYLE NAME›"

> **This is a template.** Copy it into a style directory, then replace every
> `‹angle-bracket›` placeholder and every `FILL-IN` block with concrete values.
> Anything still in angle brackets when you ship is an unfinished contract.
> Delete this banner once the file is filled in.

> **Purpose.** This is the *binding* design contract for the **‹STYLE NAME›** visual
> language. You (the implementing model — Claude, Codex, Gemini, or otherwise) did **not**
> author this visual direction; it is fixed here. Your job is to produce UI that looks as
> if it came from a single, opinionated senior designer. Do not improvise the aesthetic.
> Do not "modernize," "improve," or "DRY up" the palette, type, or structure. Follow the
> rules; deviate only where this document explicitly grants latitude — and when you do,
> log it (§16).
>
> **How to use (read in this order).**
> 1. Read the *entire* file before writing or changing any UI code. Contracts are cheap to
>    read and expensive to violate.
> 2. Treat the token block in §4 as the **single source of truth** for color, type, and
>    surface values. Reference tokens *by name*; never invent a raw hex/px in a component.
> 3. When two options are equally valid, choose the more **restrained** one.
> 4. End every UI task by running the **Compliance Checklist** (§15) against your own
>    output — verify by measurement (computed contrast, bounding rects), not by eyeballing.
> 5. Where this contract and the repo `AGENTS.md` disagree on a *visual* matter, **this
>    contract wins** (per the repo's own rule). Where they disagree on *engineering*
>    practice, `AGENTS.md` wins.
>
> **Provenance & reference implementation.** The canonical realization of this contract is
> [`‹index.html or path›`](‹index.html›) in this directory. When this document and the code
> disagree, **flag it — don't silently pick one** (§16). Treat the shipped reference as the
> ground truth for anything this document leaves ambiguous.

---

## 0. The Brief — fill this in first

> A contract without a concept is just a stylesheet. State the *idea* in plain language so
> any model can recover the intent even if it forgets a token. Keep it tight.

- **Concept (one sentence):** ‹e.g. "a deep-space instrument panel," "an heirloom ledger,"
  "descending into a dark winter sky."›
- **Emotional target (2–3 words):** ‹e.g. "quiet awe," "calm precision," "earned luxury."›
- **The single signature motif:** ‹the ONE thing a viewer remembers — a glowing line, a
  two-layer bezel, a gold rule. Everything else defers to it.›
- **Audience & domain:** ‹who this is for; what kind of product.›
- **Reference touchstones (anti-plagiarism: inspiration, not imitation):** ‹moods, eras,
  materials — not specific brands to copy.›
- **What this is NOT:** ‹name the nearest cliché you are deliberately avoiding — "not a
  fintech dashboard," "not neon techno," "not a SaaS landing page."›

---

## 1. Design philosophy (the "why," in five lines)

> Distilled from the discipline of the best: **Dieter Rams** (as little design as
> possible), **Edward Tufte** (maximize data-ink, banish chartjunk), **Apple HIG**
> (clarity · deference · depth), **Massimo Vignelli** (discipline, restraint, one type
> system), **Jan Tschichold / Müller-Brockmann** (the grid is a moral position).

1. **Restraint is the aesthetic.** The design is defined by what it omits. Every element
   must earn its place; if it doesn't carry meaning or aid a task, delete it. "Is this
   necessary?" beats "is this nice?"
2. **Content is the interface.** Typography and spacing create hierarchy — not boxes,
   borders, drop shadows, or color. Defer to the user's content; the chrome recedes.
3. **One accent, rationed.** A single accent hue, used sparingly (≤ ~10% of surface area),
   marks and guides. It never fills large regions. Meaning-colors (good/bad/warn) are
   *separate* and used only for meaning, never decoration.
4. **Tufte governs the data; Apple HIG governs the chrome.** Maximize data-ink, label
   directly, keep grids quiet (§10). Generous hit targets, content-first hierarchy,
   honest feedback (§11).
5. **Lead with the answer.** Every results view opens with the one number/statement the
   user came for (§8). Detail supports it; it never substitutes for it.

> Sanity test before shipping any screen: *"Would a senior designer call this
> overcomplicated?"* If yes, simplify. *"Would Tufte call this chartjunk?"* If yes, cut it.

---

## 2. Non-negotiables (violating any of these is a failed task)

- **Default to dark mode** with a working, persisted light/dark toggle. Both themes are
  first-class — light is never an afterthought. ‹State persistence mechanism: `localStorage`
  as `data-theme` on `<html>`, or in-memory state for sandboxed artifact builds.›
- **Tokens only.** Every color, font, radius, and spacing step comes from §4. No raw hex,
  no off-scale pixel value, no second accent hue, no unsanctioned gradient in a component.
- **One accent.** ‹name it once it's chosen.› Meaning-colors (good/danger/warn) are
  reserved for meaning. The accent is never used to color a value that carries no meaning.
- **Fonts are fixed** (§3). ‹List the chosen families.› **Forbidden as *primary/display*
  faces:** Inter, Roboto, Arial, system-ui, SF Pro, Geist — and any face that reads as a
  default. (They may appear only in fallback stacks.)
- **No pure `#000` / `#fff`** for text or fills. Use the off-tones in §4.
- **Numerals are tabular.** Any aligned numbers (tables, stat cards, axes, tooltips) use
  `font-variant-numeric: tabular-nums`; currency/percent columns right-aligned.
- **Accessibility floor (hard):** WCAG **AA** contrast (≥ 4.5:1 body text, ≥ 3:1 large
  text & UI) in *both* themes — verified by computed pairs, not eyeballed; visible
  `:focus-visible` ring on every interactive element; ≥ 44×44px touch targets (≥ 36px for
  dense icon buttons); full keyboard operability; `prefers-reduced-motion` honored; color
  is **never** the only signal.
- **i18n-ready.** All user-facing strings externalized; locale-aware dates/numbers/
  currency from the start. No hardcoded copy in markup. ‹List target locales.›
- **Responsive.** Mobile-first; verify reflow at **390 / 768 / 1280 px** with zero
  horizontal scroll and no overlap.

---

## 3. Typography

> Type does the heavy lifting. Pick **two or three families, with distinct jobs** —
> typically a *voice* face (display/headlines), a *reading* face (body/UI), and optionally
> an *instrument* face (mono, for literal data/labels). Decide the split and never cross it.

```
Voice  (headings / wordmark / hero numbers):   '‹Display Family›', ‹fallback›        (weights ‹…›)
Body   (UI / paragraphs / labels / numbers):   '‹Body Family›', ‹fallback›          (weights ‹…›)
Mono   (literal data / code / instrumentation): '‹Mono Family›', monospace          (weights ‹…›)   ← optional
```

Loaded via ‹Google Fonts `<link>` / `@import` / self-hosted›:
`‹font URL›`

### The split (the identity)

State the rule in one sentence and never break it. Example forms:
- *"Serif carries the voice; sans carries the UI; mono carries the labels."*
- *"Sans for everything you read; mono only for data you could copy-paste."*

> If a string is a **label about** data → reading face. If it **is** the data (a path, ID,
> coordinate, command) → instrument face. Headlines/body are never set in mono.

### Type scale (fluid via `clamp()`)

| Role | Face | Size | Weight | Notes |
|---|---|---|---|---|
| Hero / answer-number | Voice | `clamp(‹…›)` | ‹…› | `tabular-nums`; one per view (§8) |
| Hero H1 | Voice | `clamp(‹…›)` | ‹…› | one per page; tight line-height |
| Section H2 | Voice | `clamp(‹…›)` | ‹…› | section heads |
| Card / panel title | Voice | ‹…› | ‹…› | |
| Eyebrow / kicker | Body/Mono | ‹11–13px› | ‹600–700› | UPPERCASE, tracking ‹.04–.14em›, accent |
| Body | Body | ‹13–16px› | ‹400–500› | line-height ‹1.5–1.6› |
| Field label / caption | Body | ‹11–12px› | ‹600›  | uppercase, tracking, muted |
| Stat-card value | Body/Voice | ‹…› | ‹…› | `tabular-nums` |
| Chart tick label | Body | **‹≥11px›** | ‹400› | dedicated `tick` token (§4) |
| Chart endpoint label | Body | ‹10–11px› | ‹600› | series hue + surface halo (§10) |

### Rules

- **Minimum legible size:** no text below **‹11px›** anywhere; body base ‹≥14px›. Decide
  the floor and purge everything beneath it.
- **Hierarchy from size/weight/space**, not from boxing things.
- **Line length:** body measure 45–75 characters (`max-width: ~60ch`).
- **Line-height:** large display can run tight; body runs loose (≥1.5). Serif hero numbers
  need ≥1.15 so descenders don't clip.
- **Letter-spacing:** negative tracking on large display (‹-.02em›); positive on small
  uppercase eyebrows/labels (‹.04–.34em›).
- **The wordmark:** ‹specify face, weight, tracking, and any padding compensation.›

---

## 4. Design tokens — single source of truth  ⟵ FILL IN THE PALETTE

> **Color directives are intentionally left blank in this template.** A future designer
> fills them in here, once. Keep the *structure* and *naming discipline*; supply only the
> values. Names may be aliased per app, but **values must not diverge**. Dark first, light
> second.

### Naming conventions (keep these even when values change)

- Grounds/surfaces form a **ladder**, darkest/recessed → raised: `bg` → `surface`(/`bg1`)
  → `surface2`(/`bg2`) → raised/hover (`bg3`). State the ladder explicitly.
- Text steps: `text` (primary) → `text2` (secondary) → `text3` (muted) → a dedicated
  `tick` token for chart axes (often *higher* contrast than `text3`).
- The accent is the palette-neutral `--accent` / `--accent-soft` (avoid baking a hue name
  like `--gold` into structure, so the same skeleton can host other palettes).
- Each semantic/categorical hue ships with a translucent companion fill (e.g. `-soft` /
  `-D` at ~.10–.13 alpha) for pills, badges, and soft tiles.

```css
/* ═══ FILL IN. Dark values first, light values second. ═══ */
:root[data-theme="dark"]{
  /* Grounds — never pure #000 */
  --bg:        /* ‹page base›        */ ;
  --surface:   /* ‹cards›            */ ;
  --surface-2: /* ‹inputs/raised›    */ ;
  --bg-3:      /* ‹hover/active›      */ ;
  --border:    /* ‹card edges›        */ ;
  --border-2:  /* ‹emphasized/hover›  */ ;

  /* Text — never pure #fff */
  --text:      /* ‹primary›          */ ;
  --text-2:    /* ‹secondary›        */ ;
  --text-3:    /* ‹muted labels›     */ ;
  --tick:      /* ‹chart axis ticks ONLY — tuned for AA› */ ;

  /* Accent — the ONE accent. Rationed (§1). */
  --accent:      /* ‹marks, focus, CTA, active›          */ ;
  --accent-soft: /* ‹translucent accent fill ~.10–.13α›   */ ;
  --on-accent:   /* ‹text that sits ON an accent fill›    */ ;

  /* Semantic — meaning only, never decoration */
  --good:   /* ‹success/gain› */ ;
  --danger: /* ‹error/loss›   */ ;
  --warn:   /* ‹caution›      */ ;

  /* Categorical series — distinct HUES, not tints (max ~5–6 visible) */
  --series: /* ‹['‹c1›','‹c2›','‹c3›','‹c4›','‹c5›']› */ ;

  /* Chart chrome */
  --grid: /* ‹quiet gridline alpha, dashed› */ ;

  /* Atmosphere (optional, gradient-only — never as text/fills) */
  /* --glow / --halo: ‹…› */
}
:root[data-theme="light"]{ /* ‹mirror every token above, tuned for paper› */ }
```

**RGB triples** (keep in sync with the hexes above; used inside `rgba()` gradients/canvas):
‹accent ‹r,g,b› · … ›

### Usage rules (fill the matrix)

| Token | Allowed | Forbidden |
|---|---|---|
| `--accent` | ‹CTA fill, marks, focus ring, eyebrow rule, active state› | ‹large text, backgrounds, body copy, "decoration"› |
| `--accent-soft` | ‹soft pill/badge/tile fills, large display emphasis› | ‹small body text› |
| `--good/--danger/--warn` | ‹meaning only — gain/loss/status› | ‹decoration, theming, accents› |
| `--text-3` | ‹non-essential supporting copy› | ‹essential text, anything needing AA at small size› |
| atmosphere hues | ‹inside gradients only› | ‹text, borders, fills› |

> **Text-on-accent rule (mandatory).** Any text sitting on an accent fill is `--on-accent`
> — never a translucent/light text token. Light accents demand a dark `--on-accent`; verify
> the computed pair passes AA. (This is the single most common contrast bug — pin it in CSS
> so specificity can't override it.)

> **Surfaces.** Cards = `--surface` + 1px `--border`, radius ‹…›. Shadows are rare and
> soft; dark mode prefers *surface contrast over shadow*. Glows (if used) are **colored and
> radial**, never gray decorative drop shadows.

---

## 5. Spacing & layout

- **Spacing scale:** a 4px (or 8px) grid. Lean on the ‹4/8/12/16/20/24/32› rhythm; no
  off-scale magic numbers. Space is the luxury — be generous with section rhythm
  (`padding-block: clamp(‹…›)`).
- **Container:** `width: min(‹1240px›, 90vw); margin-inline: auto;` (state the max width).
- **Radius scale:** ‹enumerate: inputs ‹…› · cards ‹…› · hero ‹…› · pills `100px`.›
- **Grid is the backbone.** Compose on a consistent column grid; align to it. Asymmetry is
  allowed and encouraged as a deliberate device — centered-everything is a smell except for
  the one or two climactic moments you *choose* to center.
- **Control-height parity.** Adjacent controls (input, select, segmented, button) share an
  identical height — measure equal via bounding rects (±0px), not "close." Min control
  height ≥ 44px with `box-sizing: border-box`. Native `<select>` chevrons desync heights —
  use `appearance:none` + a token-colored SVG chevron.
- **Equal-height rows.** Let grid cells stretch to row height; don't opt out. Divider-style
  grids must not expose the gap color as a slab on an incomplete final row.
- **No overlap, no crowding — clearance is computed, not eyeballed.** Absolutely-positioned
  annotations (labels, badges, tooltips) reserve layout headroom for their full extent and
  sit ≥ 8px from unrelated text/controls. Tooltips/popovers `position:fixed`,
  viewport-clamped, flip when there's no room. Verify against bounding rects.
- **Edge instrumentation (optional signature):** pinned mono micro-labels framing the
  viewport like a viewfinder — use only if it serves the concept.

---

## 6. Components (match the reference; don't invent parallel ones)

> Build from the reference implementation's recipes. If a needed component doesn't exist,
> design it *in the established idiom* and document it here.

- **Card** — `--surface`, 1px `--border`, radius ‹…›; emphasis via a ‹3px accent left/top
  strip›, not a new hue. Hover = ‹subtle lift / border warm›.
- **Inputs** — `--surface-2` fill, 1px border, radius ‹…›; focus = accent border +
  `0 0 0 3px var(--accent-soft)` ring; `tabular-nums`; ≥16px font on iOS-facing inputs
  (prevents zoom); ≥44px height (§5).
- **Buttons** — primary = ‹accent fill + `--on-accent` text›; secondary/ghost = ‹border +
  accent text›; danger = ‹`--danger`›. Every button has hover, focus-visible, active, and
  disabled states.
- **Segmented control** — pill group on `--surface-2`; active segment filled accent with
  `--on-accent` text.
- **Stat card / metric** — uppercase muted label over a ‹large weighted› `tabular-nums`
  value; color the value *only* when it carries meaning.
- **Badges / chips** — radius-full, small; status/category use the soft companion fill +
  solid hue text (+ optional 1px hue border); neutral chips use `--surface-2` + `--border`.
- **Tables** — header uppercase muted with tracking; numbers right-aligned `tabular-nums`;
  quiet row rules; multi-column comparisons use `table-layout: fixed` for equal widths.
- **Icons** — one family, consistent stroke (‹1.5–2px›). Don't mix icon sets. Decorative
  glyphs/emoji only where the reference already uses them; never as interactive icons.
- **States are mandatory:** every data surface defines **empty**, **loading**, and
  **error** states — never a blank pane. Empty = one muted line + one clear action.

---

## 7. Theme system & the toggle

- Dark is the default and is applied as `data-theme` on `<html>` ‹before first paint to
  avoid a flash›. Persist the choice (§2).
- **Both themes are designed, not derived.** Tune light independently — don't just invert.
  Re-check contrast, halo/glow colors, soft-fill alphas on white, and thin dashed lines in
  *both* themes.
- ‹If applicable:› an `@media print` override forces a legible light ink palette, hides
  chrome, expands collapsed content, and restores any `content-visibility` so nothing
  prints blank.

---

## 8. The lead readout (mandatory for results)

Every results view leads with **one dominant answer** — the thing the user came to learn
("Lifetime savings $184,000", "Risk score 72 / 100"). Detail (tables, charts, gauges)
sits *below* and supports it.

Anatomy (adapt to the style):

```
┌─ card: --surface, 1px --border, ‹accent edge›, radius ‹…›, generous padding ─┐
│ EYEBROW        small / bold / uppercase / tracked / accent                   │
│ 184,000        Voice face, large, tabular-nums  ← the answer-number          │
│ context line   body, --text-2                                                │
│ chip · chip    uppercase muted key + colored value (color = meaning only)    │
└──────────────────────────────────────────────────────────────────────────────┘
```

- **Color discipline:** the big number stays neutral (`--text`) unless its *sign* is the
  meaning (a loss → `--danger`, a credit → `--good`). The accent belongs to the eyebrow,
  not the number.
- **Breathing room:** the number never touches or clips a card edge; verify with bounding
  rects. Serif numbers need `line-height ≥ 1.15`.

---

## 9. Motion grammar

- **One shared easing** everywhere: `--ease: ‹cubic-bezier(…)›`. **Tempo:** ‹slow &
  orchestrated / quick & functional — pick one and commit.›
- **Durations:** chrome transitions ‹.15–.3s›; reveals ‹~1s›; ambient loops ‹6–14s›.
- **One signature motion**, applied consistently (a staggered page-load reveal, a digit
  roll on hero numbers, an animated gauge fill — pick the ONE that fits §0 and name it).
  Everything else is calm.
- **Scroll reveals** fire **once** (`IntersectionObserver`, unobserve after firing) — never
  replay on scroll-back.
- **`prefers-reduced-motion: reduce` is mandatory** → disable animation, snap to resting
  state, suppress ambient/decorative motion. Content must be fully legible static.
- **Forbidden:** bounce, spring overshoot used as decoration, parallax, attention-grabbing
  micro-bounces, anything fast and springy (unless §0 explicitly calls for it).

---

## 10. Data visualization — Tufte's rules (the heart of this contract)

> **Strictly follow Edward Tufte.** The graphic exists to let the reader *think about the
> data*, not about the graphic. These rules are not stylistic preferences — they are the
> contract.

**Tufte's principles, enforced:**

1. **Maximize the data-ink ratio.** Every drop of ink should present data. Erase
   non-data-ink (heavy gridlines, borders, backgrounds, tick marks) and redundant
   data-ink. If erasing it loses no information, erase it.
2. **Banish chartjunk.** No 3D, no bevels, no drop shadows on bars, no moiré/hatching, no
   decorative gradients, no rainbow palettes, no gratuitous color. Zero "ducks."
3. **Tell the truth — `Lie Factor ≈ 1`.** The size of the effect shown must match the size
   of the effect in the data. Bar/area charts start at a **zero baseline**; never truncate
   an axis to exaggerate. Areas encode one variable, not two.
4. **High data density; small multiples.** Prefer many small, comparable panels sharing
   scales and axes over one busy chart. Comparison is the engine of insight.
5. **Direct labeling over legends.** Label series at their final data point (series hue,
   small bold, with a surface-colored `paint-order: stroke` **halo** so the label survives
   over gridlines). Keep a compact legend only as colorblind/mobile redundancy.
6. **Annotate reference lines on the chart.** Thresholds/targets are dashed and carry an
   inline label with **name *and* value** ("Target · $212k") — never legend-only, never a
   bare 1px line.
7. **The range-frame / minimal axes.** Quiet gridlines (use the `--grid` token, dashed,
   horizontal-only where sensible); raise *label* contrast (the `--tick` token), never grid
   loudness. Show ticks only where data exists. Consider sparklines for inline trends.
8. **Series hierarchy.** The primary series is the loudest (thickest/solid); context series
   are thin/dashed/lower-opacity. The eye must find the answer first.
9. **Distinct hues, not tints.** Two series are never tints of one hue. Use redundant
   encoding (hue + dash/shape) for adjacent series and for colorblind safety.
10. **Bars and bands carry their values.** Bars get value labels at their ends/segments;
    confidence intervals are honest **range areas** (low–high), filled at low opacity with
    no stroke — never a faked mask.
11. **Tooltips** match the surface recipe (`--surface` + 1px `--border`, small radius,
    `tabular-nums`, formatted units).
12. **Number formatting is honest and consistent.** Significant digits appropriate to
    precision; thousands separators; units stated once; locale-aware.

> **Library note.** ‹Recharts / hand-built CSS+SVG / D3 — state the chosen viz stack.›
> If SVG `fill`/`stroke` don't inherit CSS vars in your setup, mirror the §4 hexes into the
> chart config and keep them in sync — don't "fix" them to vars and break rendering.

---

## 11. Accessibility & Apple HIG (the floor, not the ceiling)

> **Strictly follow the [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/)**
> and **[WCAG 2.2 AA](https://www.w3.org/WAI/WCAG22/quickref/)**.

**Apple's three pillars:**
- **Clarity** — legible at every size; precise, unambiguous icons; content over chrome.
- **Deference** — the UI defers to content; no chrome competes with the data.
- **Depth** — hierarchy and (restrained) layering communicate structure and state.

**HIG practices to honor:** consistency (same action looks/behaves the same everywhere);
immediate, honest feedback for every action; clear affordances (interactive things look
interactive); forgiveness (confirm destructive actions; support undo); progressive
disclosure (don't dump everything at once); respect platform conventions and safe areas.

**Accessibility floor (verify, don't assume):**
- **Contrast:** body text ≥ 4.5:1; large text (≥ ‹18.66px bold / 24px›) and UI components
  ≥ 3:1 — in *both* themes, by computed pairs. Aim for **AAA (≥ 7:1)** on primary body text
  where the palette allows.
- **Color is never the only signal.** Pair every color-coded meaning with a glyph, label,
  pattern, or position.
- **Keyboard:** every interactive element reachable and operable by keyboard; logical tab
  order; visible `:focus-visible` ring; no keyboard traps; skip-to-content link.
- **Touch:** targets ≥ 44×44px (≥ 36px dense icon buttons), with adequate spacing.
- **Semantics:** real landmarks (`<nav> <main> <header> <section> <footer>`), one `<h1>`
  per page, ordered headings, `<button>` for actions and `<a>` for navigation, `aria-label`
  on icon-only controls, `aria-live` for async updates, labelled form fields.
- **Motion:** honor `prefers-reduced-motion`; no content conveyed by motion alone; nothing
  flashes > 3×/sec.
- **Zoom/reflow:** legible and functional at 200% zoom and at 390px width with no loss of
  content or horizontal scroll.
- **Respect** `prefers-color-scheme`, `prefers-contrast`, and reduced-transparency where
  feasible.

---

## 12. Content, voice & microcopy

- **Voice:** ‹2–3 adjectives — e.g. "precise, calm, never cute."› Define it so copy is
  consistent across models.
- **Microcopy:** concise, specific, human. Labels are nouns; buttons are verbs. No filler,
  no exclamation marks, no dark patterns.
- **Numbers & dates:** locale-aware formatting; consistent precision and units; tabular
  alignment.
- **Empty/error/loading copy:** say what happened and what to do next — one line, one
  action. Never blame the user.
- **i18n:** every string externalized into the dictionary; write each locale natively, not
  machine-translated; never concatenate translated fragments.

---

## 13. Performance & build budget

- **Budget:** ‹state targets — e.g. ≤ ‹X›KB CSS/JS, LCP < 2.5s, CLS < 0.1, no layout
  shift from late-loading fonts (`font-display: swap` + sized fallbacks).›
- **Fonts:** subset/preconnect; the stack must degrade legibly if the CDN fails — don't
  hard-depend on it for legibility.
- **Images/media:** correct dimensions, lazy-load below the fold, modern formats.
- **Long lists:** `content-visibility: auto` + `contain-intrinsic-size` for large repeated
  rows — but restore visibility inside `@media print`.
- **Listeners:** `passive` scroll/resize; cap canvas DPR (≤2); static layers stay fixed.
- **Stack discipline:** ‹state the sanctioned stack — e.g. "single self-contained
  `index.html`, zero build, fonts from Google Fonts only" or "shadcn/ui + Tailwind +
  Recharts."› Add no library the task didn't require.

---

## 14. Anti-patterns — DO NOT

- ❌ Introduce a new hue, a second accent, or a decorative gradient. One accent, full stop.
- ❌ Use a forbidden default face (§2) as a primary/display font, or cross the font split.
- ❌ Pure `#000` / `#fff` text or backgrounds. Use the §4 off-tones.
- ❌ Raw hex/px in a component instead of a token; a magic number off the spacing scale.
- ❌ Color a value that carries no meaning; use a meaning-color (good/danger/warn) as decor.
- ❌ Translucent/light text on an accent fill (use `--on-accent`); illegible focus states.
- ❌ Chartjunk: 3D, bar shadows, heavy gridlines, rainbow palettes, truncated baselines,
  legend-only thresholds, two series as tints of one hue, unlabeled bars.
- ❌ Decorative motion: bounce, parallax, springy micro-interactions; animating anything
  while ignoring `prefers-reduced-motion`.
- ❌ Ship a dark-only or light-only build, or let either theme fail AA.
- ❌ Convey status by color alone.
- ❌ Eyeball clearance/contrast/alignment — measure it.
- ❌ Hardcode user-facing strings; concatenate translated fragments.
- ❌ "DRY up" duplicated tokens into a shared package if self-containment is the constraint;
   "improve" the palette/type; or silently resolve a doc-vs-code conflict (§16).

---

## 15. Compliance checklist (run before declaring done)

- [ ] Dark is default; light/dark toggle works and persists; **both** themes checked
      deliberately (contrast, halos, thin dashed lines, soft fills on white).
- [ ] Zero raw hex/px outside §4; everything maps to a token; one accent only;
      meaning-colors only carry meaning.
- [ ] Fonts per §3; the font split is never crossed; `tabular-nums` on all aligned figures;
      no text below the §3 floor.
- [ ] Every text/background pair clears WCAG **AA** in both themes — by computed contrast,
      not eyeballed; text on accent fills uses `--on-accent`.
- [ ] Results lead with a single answer-readout (§8); value colored only when meaningful.
- [ ] Charts obey Tufte (§10): quiet grids + `--tick` labels; primary series loudest;
      thresholds dashed with inline name+value; series directly labeled with halo; bars
      value-labeled; bands are honest range areas; zero baseline; distinct hues not tints;
      no chartjunk.
- [ ] Apple HIG honored (§11): clarity/deference/depth; consistent, forgiving, immediate
      feedback; affordances clear.
- [ ] Keyboard-complete; visible focus rings; ≥44px hit targets; semantic landmarks; color
      never the sole signal; `prefers-reduced-motion` honored.
- [ ] Empty / loading / error states present on every data surface.
- [ ] No overlap or crowding: absolute annotations have computed headroom ≥8px from
      neighbors; control-height parity verified via bounding rects; comparison columns equal
      width; equal-height grid rows.
- [ ] Motion: one shared easing; the single signature motion applied consistently; reveals
      fire once; no bounce/parallax.
- [ ] i18n: new strings in every locale dictionary, written natively.
- [ ] Performance/build budget (§13) met; verified at **390 / 768 / 1280 px** with no
      horizontal scroll.
- [ ] Any deviation from this contract is logged in §16 (not silently applied).

---

## 16. Governance — handoff, provenance & change log

> This is what makes the contract *binding across LLMs*. A design language survives handoff
> only if intent and changes are recorded. Keep this section current.

**The handoff protocol (every model, every task):**
1. **Read** the whole contract + skim the reference implementation before editing.
2. **Reference by token**, never by raw value.
3. **When the contract is silent**, defer to the reference implementation; if still
   ambiguous, choose the more restrained option and note the decision below.
4. **When the contract and the code disagree, FLAG IT** in the conflict log — never
   silently pick one.
5. **When you must deviate** from a rule, you need an explicit reason; record it as a
   decision below with date, scope, and rationale. Unlogged deviations are contract
   violations.
6. **When you change a token or rule**, update §4/the relevant section *and* the change log
   in the same commit, and update every place the token is duplicated (see the map below).

**Token / source-of-truth map** (where each thing lives — keep in sync):

| Concern | Home |
|---|---|
| Color / surface / text tokens | ‹`[data-theme]` blocks in `‹file›` at ‹location›› |
| Type scale & font loading | ‹`<head>` `<link>` + CSS `:root` in `‹file›`› |
| Categorical series palette | ‹`‹array/object›` in `‹file›`› |
| Theme state | ‹persistence mechanism + where applied› |
| Print palette | ‹`@media print` block in `‹file›`› |
| Reference implementation | [`‹index.html›`](‹index.html›) |

**Decision log** (deviations & rationale — append, never rewrite history):

| Date | Model | Decision / deviation | Rationale | Scope |
|---|---|---|---|---|
| ‹YYYY-MM-DD› | ‹model› | ‹what changed/deviated› | ‹why it was justified› | ‹files/components› |

**Conflict log** (contract ⇄ code mismatches awaiting a human ruling):

| Date | Where | Contract says | Code does | Status |
|---|---|---|---|---|
| ‹YYYY-MM-DD› | ‹§ / file› | ‹…› | ‹…› | ‹open / resolved› |

**Change log** (versioned edits to this contract):

| Date | Version | Change |
|---|---|---|
| ‹YYYY-MM-DD› | ‹0.1› | Initial contract authored from the template. |
