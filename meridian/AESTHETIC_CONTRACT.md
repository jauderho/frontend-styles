# AESTHETIC CONTRACT — "Meridian"

> The binding design contract for the **Meridian** design language.
> Read this before writing or changing any UI in this directory. It fixes the
> concept, palette, typography, atmospheric layers, motion grammar, component
> anatomy, and tokens. Where this contract and the repo `AGENTS.md` disagree on
> visual matters, **this contract wins** (per the repo's own rule).

---

## 1. The Concept

**Meridian** is a cinematic, editorial, dark-luxury aesthetic built around a single
idea: **descending into the dark.** Its canonical palette is **Celestine** — a glacial,
near-monochrome winter night: deep slate-blue grounds, a cold ice-blue accent, and a
cool moonlit white for type. It was authored for a fictional private observatory and
stargazing retreat, but the language generalizes to any premium, nocturnal,
contemplative brand — luxury hospitality, audio, fragrance, astronomy, slow travel,
high-end editorial.

The emotional target is **quiet awe.** It is not loud, not neon, not "techy." It is the
feeling of standing under a sky so dark the Milky Way is loud, in air cold enough to see
your breath. Restraint is the governing instinct: generous negative space, one signature
motif, a rationed accent.

### Non-negotiable principles

1. **One conceptual motif, executed precisely.** The signature is the glowing vertical
   *meridian line* + a living starfield. Everything else defers to it.
2. **The accent is rationed, never a field.** The ice-blue accent is < ~8% of the
   surface area. It marks, it never fills large regions.
3. **Atmosphere over flat fills.** Backgrounds are layered radial gradients + grain,
   never a single solid color.
4. **Serif carries the voice; mono carries the labels.** Display serif is the brand.
   Monospace is the instrumentation (coordinates, eyebrows, metrics).
5. **Motion is slow and orchestrated.** One staggered page-load, gentle scroll reveals,
   ambient drift. Nothing bounces. Nothing is fast.

### Forbidden (anti-slop guardrails)

- ❌ Inter, Roboto, Arial, system-ui as the *display* face.
- ❌ Purple-gradient-on-white, or any light-mode default.
- ❌ Evenly distributed rainbow palettes; "timid" color.
- ❌ Hard pure-black `#000` or pure-white `#fff` for text or fields.
- ❌ Fast, springy, or attention-grabbing micro-bounces.
- ❌ Box-shadow drop shadows used as decoration (glow is radial and colored, not gray).

---

## 2. Color

Dark, always. **Celestine** is a glacial sky: deep slate-blue-black grounds, a cold
ice-blue accent (moonlight on snow), a periwinkle and a cyan for atmospheric gradients,
and a cool moonlit white for text. The palette is deliberately close to monochrome —
its elegance comes from a narrow, cold hue range, not contrast of hues.

> **Token naming.** The accent is the palette-neutral `--accent` / `--accent-soft` (so
> the same structure can host other palettes without misleading names). Everything else
> keeps its semantic name. The historical `--gold` name is retired.

### CSS custom properties (canonical source of truth)

```css
:root{
  /* Grounds — slate-blue-blacks, never pure #000 */
  --ink:        #060a12;   /* page base */
  --night:      #0a1424;   /* top-of-sky / elevated surface */
  --indigo:     #0f1c30;   /* hover surface */
  --indigo-2:   #182840;   /* deepest elevated surface */

  /* Accent — cold ice-blue (moonlight). Use sparingly. */
  --accent:      #8fbfe6;  /* primary accent, CTA fill, marks */
  --accent-soft: #c2e0f5;  /* serif highlight, large display emphasis */

  /* Atmosphere — only ever inside gradients, never as text/fills */
  --rose:       #7c8fd4;   /* periwinkle (the "warm" pole of a cold palette) */
  --dawn:       #5fa8c4;   /* glacial cyan */

  /* Ink-on-dark — cool moonlit white, never pure #fff */
  --cream:      #eaf1f8;   /* primary text */
  --muted:      rgba(234,241,248,.56);  /* secondary text */
  --faint:      rgba(234,241,248,.14);  /* borders on interactive elements */
  --line:       rgba(234,241,248,.10);  /* hairline dividers, card borders */
}
```

**RGB triples** (used directly inside `rgba()` gradients/canvas — keep in sync with the
hexes above): accent `143,191,230` · cyan/`--dawn` `95,168,196` · periwinkle/`--rose`
`124,143,212` · text/`--cream` `234,241,248`.

### Usage rules

| Token | Where it is allowed | Where it is forbidden |
|---|---|---|
| `--accent` | CTA fill, the meridian line, marks (`✦`), small icons, eyebrow rules, idx numbers | large text blocks, backgrounds, body copy |
| `--accent-soft` | italic emphasis inside large display serif, stat numbers, hover-warmed text | anything below ~1.5rem |
| `--rose`, `--dawn` | **only** as color stops inside radial gradients | text, borders, fills |
| `--cream` | all primary text | backgrounds |
| `--muted` | secondary copy, labels, captions | headlines, CTAs, **text on a light accent** |
| `--ink`/`--night` | grounds & surfaces | text |

**Contrast:** `--cream` on `--ink` ≈ 15:1. `--muted` (.56 alpha) is reserved for
non-essential supporting text only. The accent is *light*, so **text placed on top of an
accent fill must be `--ink`, never `--muted`/`--cream`** (see the button rule in §7.1).
`--accent` as text on `--ink` passes AA at ≥ ~1.3rem; below that it is for non-text marks.

---

## 3. Typography

A distinctive optical-size serif for voice, a clean humanist grotesque for body, a
monospace for instrumentation. **Three families, three jobs.**

```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300..700;1,9..144,300..600&family=Spline+Sans:wght@300;400;500;600&family=Spline+Sans+Mono:wght@400;500&display=swap" rel="stylesheet">
```

```css
:root{
  --display: "Fraunces", serif;                       /* voice */
  --body:    "Spline Sans", system-ui, sans-serif;    /* reading */
  --mono:    "Spline Sans Mono", monospace;           /* instrumentation */
}
```

### Roles

- **Fraunces (display)** — every headline, blockquote, brand wordmark, stat number,
  marquee text. Weights **330–360** (deliberately light). `font-optical-sizing: auto`.
  Italic is a feature: use `font-style: italic` on the emphasized phrase, recolored to
  `--accent-soft`. Negative tracking on large sizes (`-.02em` to `-.01em`).
- **Spline Sans (body)** — paragraphs, lede, nav links, footer copy. Weight **300** for
  lede/large copy, **400** default. Generous `line-height: 1.6`.
- **Spline Sans Mono (instrumentation)** — eyebrows, coordinates, metric labels, CTA
  text, footer legal, section meta. **Always** uppercase with wide tracking
  (`.14em`–`.34em`). This is the "scientific instrument" voice.

### Type scale (fluid, `clamp()`)

| Token | Size | Use |
|---|---|---|
| Hero H1 | `clamp(3rem, 9.5vw, 8.4rem)` / `line-height:.96` | one per page |
| Section H2 | `clamp(2.2rem, 5.2vw, 4.2rem)` / `1.02` | section heads |
| Reserve/CTA H2 | `clamp(2.4rem, 6vw, 5rem)` / `1.0` | climactic CTA |
| Card H3 | `clamp(1.7rem, 3.2vw, 2.6rem)` / `1.04` | offering titles |
| Blockquote | `clamp(1.8rem, 4.6vw, 3.6rem)` / `1.18` italic | pull quotes |
| Stat number | `clamp(2.6rem, 5vw, 3.8rem)` | metrics |
| Lede | `clamp(1rem, 1.4vw, 1.18rem)` wt 300 | hero subcopy |
| Eyebrow / label | `.66rem`–`.74rem`, mono, `.14em`–`.34em` tracking, uppercase | everywhere |

### The wordmark

`MERIDIAN` in `--display`, weight 500, **letter-spacing `.42em`** with matching
`padding-left:.42em` (so the tracking doesn't shift it off-axis). The footer wordmark
is the same at `2.6rem` / `.3em`.

### The eyebrow component

Mono, uppercase, `.34em` tracking, color `--accent`, preceded by a 26px accent hairline:

```css
.eyebrow{ font-family:var(--mono); font-size:.72rem; letter-spacing:.34em;
  text-transform:uppercase; color:var(--accent); display:inline-flex; gap:.7em; align-items:center; }
.eyebrow::before{ content:""; width:26px; height:1px; background:var(--accent); opacity:.6; }
```

---

## 4. Atmosphere (the four background layers)

Meridian backgrounds are **composed, never flat.** Four fixed layers, back to front:

1. **`.sky`** (`z-index:-3`) — the gradient ground. Stacked radial gradients (cold accent
   glow top-right, glacial cyan top-left, periwinkle bottom) over a vertical
   night→ink→near-black linear gradient.

   ```css
   .sky{ position:fixed; inset:0; z-index:-3;
     background:
       radial-gradient(140% 90% at 78% -10%, rgba(143,191,230,.16) 0%, transparent 42%),
       radial-gradient(120% 80% at 12% 8%, rgba(95,168,196,.20) 0%, transparent 46%),
       radial-gradient(100% 120% at 50% 120%, rgba(124,143,212,.14) 0%, transparent 50%),
       linear-gradient(178deg, var(--night) 0%, var(--ink) 38%, #030610 100%); }
   ```

2. **`#stars`** (`z-index:-2`) — a `<canvas>` starfield (see §6).
3. **`.grain`** (`z-index:50`) — SVG `feTurbulence` fractal noise, `opacity:.05`,
   `mix-blend-mode:overlay`. Sits *above* content to unify the image into one frame.

   ```css
   .grain{ position:fixed; inset:0; z-index:50; pointer-events:none;
     opacity:.05; mix-blend-mode:overlay;
     background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E"); }
   ```

4. **`.cursor`** (`z-index:40`) — a soft radial ice-blue glow that trails the pointer with
   easing (desktop/`hover` pointers only), `mix-blend-mode:screen`. See §6.

Glows everywhere are **colored and radial** (`rgba(accent/cyan,…)`), never gray drop
shadows. Card and CTA "shadows" are accent-tinted: `0 14px 40px -12px rgba(143,191,230,.55)`.

---

## 5. Layout & Spatial System

- **Container:** `.wrap { width: min(1240px, 90vw); margin-inline: auto; }`
- **Section rhythm:** `padding-block: clamp(6rem, 12vh, 11rem)`. Space is the luxury.
- **Section head** is a two-column baseline-aligned split: a left H2 (`max-width:16ch`,
  with one italic accent phrase) and a right supporting paragraph (`max-width:34ch`,
  `--muted`). Collapses to stacked on narrow screens.
- **Asymmetry & grid-breaking:** the hero content is left-weighted within a max
  `60rem` grid; the moon orb bleeds toward the top-right edge; offering cards translate
  on hover. Avoid centered-everything except for the deliberate climactic moments
  (the quote and the reserve card, which *are* centered for contrast).
- **Radii:** stat grid `14px`, cards `16px`, reserve card `24px`, pills/CTAs `100px`.
- **Hairlines:** all dividers and card borders are `1px solid var(--line)`; interactive
  borders are `var(--faint)`, warming to `rgba(143,191,230,.4)` on hover.
- **Edge instrumentation:** absolutely-positioned mono micro-labels pinned to viewport
  corners (coordinates bottom-left, vertical "scroll cue" bottom-right). This is a
  signature — treat the frame like a viewfinder.

---

## 6. Motion Grammar

**Easing:** one shared curve everywhere — `--ease: cubic-bezier(.16,1,.3,1)`.
**Tempo:** slow. Reveals ~1s, hovers .3–.5s, ambient loops 6–14s.
**Always** honor `prefers-reduced-motion` (see §8).

### Page-load (orchestrated, once)

Hero children carry `.reveal` + `data-stagger` with `--i` index; transition-delay is
`calc(var(--i) * 90ms)`. They rise 30px and fade in. This is the single most important
delight moment — get the stagger right.

```css
.reveal{ opacity:0; transform:translateY(30px);
  transition:opacity 1s var(--ease), transform 1s var(--ease); }
.reveal.in{ opacity:1; transform:none; }
[data-stagger]{ transition-delay:calc(var(--i,0) * 90ms); }
```

### Scroll reveals

`IntersectionObserver`, `threshold:.12`, `rootMargin:'0px 0px -8% 0px'`, **unobserve
after firing** (reveal once, never replay).

### Ambient (infinite, subtle)

- **Meridian line** `breathe` — opacity .45↔.95 over 6s.
- **Moon** `floaty` — `translateY(0↔-16px)` over 14s.
- **Marquee** `scroll` — `translateX(0→-50%)` over 38s linear; **pause on hover**;
  edges masked with a transparent→opaque→transparent `mask-image`.
- **Scroll cue** `drop` — a 1px accent line that scales vertically, 2.2s.

### Canvas starfield (`#stars`)

- Density `~ (w·h)/6500` stars; DPR-capped at 2.
- Three star hues, weighted: ~18% accent `143,191,230`, then ~50/50 cool-white
  `234,241,248` / pale steel `190,210,235`. Each twinkles via an alpha oscillation.
- **Shooting star:** low-probability spawn (~1.2%/frame) when none active; a cool-white
  `234,241,248` gradient streak that travels down-right, fading out. Disabled under
  reduced-motion.
- Re-seeds on resize. `pointer-events:none`.

### Cursor glow (`.cursor`)

340px radial ice-blue glow `rgba(143,191,230,.16)`, `screen` blend, lerped toward pointer
at `.14` per frame. Removed entirely on `(hover:none)` (touch). Body sets `cursor:none` on
desktop; restored to `auto` under `(hover:none)`.

### Hover signatures

- **Primary CTA** (`.btn`): ice-blue pill; an `--accent-soft` layer wipes up from
  `translateY(101%)` to `0`; lifts `-2px`; gains an accent-tinted glow. Label sits in a
  `z-index:1` `<span>`.
- **Ghost CTA** (`.btn-ghost`): transparent, `--faint` border, faint cool-white wipe
  `rgba(234,241,248,.06)`, no lift/glow.
- **Offering card**: border warms to accent, whole card `translateX(8px)`, a corner
  accent radial wash fades in, and the `↗` arrow nudges `translate(5px,-5px)`.
- **Nav links**: an accent underline grows from width 0 → 100%; color → `--cream`.
- **Stat cell**: ground shifts `--ink` → `--indigo`.

---

## 7. Component Library

### 7.1 Nav

Fixed, transparent at top. On `scrollY > 40` adds `.shrink`: reduced vertical padding,
`rgba(6,10,18,.72)` + `backdrop-filter:blur(14px)`, and a `--line` bottom border.
Left: tracked wordmark. Right: link cluster + one primary CTA pill. Below 860px the
link cluster hides and a `☰` toggle appears (the toggle is currently presentational —
wire it up if the app needs a real menu).

> **Button legibility rule (mandatory).** `.navlinks a` sets `color: var(--muted)` for the
> text links, which by specificity overrides `.btn`'s `color: var(--ink)`. Left unchecked,
> the nav CTA renders translucent text on a *light* accent fill — illegible. Pin it:
> ```css
> .navlinks a.btn{ color:var(--ink); }
> ```
> General principle: **any text sitting on an accent fill is `--ink`.**

### 7.2 Hero

`min-height:100svh`, vertically centered. Contains the **meridian line** (1px vertical
accent gradient down `left:50%`, glowing `rgba(143,191,230,.5)`, breathing), the **moon**
orb (cool blue-white radial sphere `#f4f9ff→#d4e4f2→#a0bcd6→#6f8aa8` with a cold inset
shadow `rgba(15,35,60,.55)` and accent glow, floating), the staggered text stack (eyebrow
→ H1 with one italic-accent phrase and one `--muted` phrase → lede → CTA row), and the
corner instrumentation (coords, scroll cue).

### 7.3 Marquee strip

Full-bleed, top/bottom `--line` borders, faint lighten background. Infinite track of
Fraunces-italic phrases separated by accent `✦` marks. Content is **duplicated** so the
`-50%` translate loops seamlessly. Masked edges. Pauses on hover.

### 7.4 Stat grid

4 columns on a `1px`/`--line` gap (so the gap reads as hairline rules), `14px` radius,
clipped. Each cell: Fraunces `--accent-soft` number (units as a small inline span) + mono
uppercase label. Hover warms the cell ground.

### 7.5 Offering card

`grid-template-columns: auto 1fr auto`: mono index (`01`/`02`/`03`) · title+body ·
right-aligned mono meta with `↗`. Border + corner glow + `translateX` on hover. Below
860px drops to two columns and hides the meta column.

### 7.6 Pull quote

Centered. Fraunces italic, `max-width:20ch`, with `<b>` phrases in `--accent-soft` (still
italic, still weight ~330). Mono `cite` beneath, uppercase, `.2em` tracking.

### 7.7 Reserve card (the climax)

Rounded `24px` glass card: layered accent + cyan radial washes
(`rgba(143,191,230,.12)`, `rgba(95,168,196,.16)`) over `rgba(10,20,36,.6)` with
`backdrop-filter:blur(6px)`. Centered stack: eyebrow → big H2 with italic-accent word →
paragraph → primary CTA → a mono "season" row of `label · value` facts where the value is
`--cream` weight 500 and the label is `--muted`.

### 7.8 Footer

`--line` top border. Flex row: oversized tracked wordmark + tagline on the left; three
columns of links with accent mono headings. A bottom sub-row (own `--line` border) carries
mono copyright on the left and coordinates on the right — closing the viewfinder frame.

---

## 8. Accessibility & Responsiveness

- **Reduced motion is mandatory.** `@media (prefers-reduced-motion:reduce)` disables
  *all* animation (`animation:none !important`), forces `.reveal` to its resting state,
  and the starfield suppresses shooting stars. Content must be fully legible static.
- **Touch.** `(hover:none)` removes the cursor glow and restores `cursor:auto`; all
  hover affordances must have a usable resting state (they do).
- **Breakpoints.** Verify at **390px, 768px, 1280px**. Defined behavior:
  - `≤860px`: nav links → `☰`; stat grid 4→2; offering card 3→2 cols, meta hidden;
    moon bleeds off-edge at reduced opacity; scroll cue hidden.
  - `≤480px`: stat grid → 1 col; one trailing coordinate hidden.
- **Semantics.** Real landmarks (`<nav> <header> <section> <footer>`), `<article>` per
  offering, `<blockquote>`/`<cite>`, `aria-label` on icon-only controls.
- **Color is never the only signal**; borders, position, and motion reinforce state.
- **Text on accent fills is `--ink`** — never a translucent/light token (see §7.1).
- **Performance.** Canvas DPR-capped at 2; scroll/resize listeners `passive`; reveals
  unobserved after firing; gradients/grain are static fixed layers.
- **Offline/fallback.** Fonts load from Google Fonts CDN; the stack degrades to
  `serif`/`system-ui sans`/`monospace`. Don't hard-depend on the CDN for legibility.

---

## 9. Recreation Checklist

Use this to verify any Meridian surface is on-contract:

- [ ] Dark slate-blue ground via **layered radial + linear gradients** — not a solid color.
- [ ] Grain overlay present (`opacity:.05`, `overlay` blend) above content.
- [ ] Living **canvas starfield** (twinkle + occasional shooting star), reduced-motion aware.
- [ ] The **meridian line** or an equally singular signature motif is present.
- [ ] Fraunces display (wt 330–360, optical sizing, italic-accent emphasis) for all headings.
- [ ] Spline Sans body (wt 300/400); Spline Sans Mono for **all** eyebrows/labels/coords (uppercase, wide tracking).
- [ ] Accent (`--accent`) is rationed (≤ ~8% surface); periwinkle/cyan appear **only** inside gradients.
- [ ] No pure `#000`/`#fff`; text is `--cream`/`--muted`.
- [ ] **Text on any accent fill is `--ink`** (nav CTA pinned via `.navlinks a.btn`).
- [ ] Single shared easing `cubic-bezier(.16,1,.3,1)`; slow tempo; one staggered page-load.
- [ ] Scroll reveals fire **once** (unobserve after).
- [ ] Generous section rhythm (`clamp(6rem,12vh,11rem)`), `min()`-based container.
- [ ] Corner instrumentation (coordinates / scroll cue) framing the viewport.
- [ ] CTA = accent pill with upward color-wipe + lift + accent glow; ghost variant for secondary.
- [ ] `prefers-reduced-motion`, `(hover:none)`, and 390/768/1280 breakpoints all handled.
- [ ] Glows are colored & radial; no gray decorative drop shadows.

---

## 10. Token Quick-Reference

```css
/* paste-ready core — Meridian / Celestine */
:root{
  --ink:#060a12; --night:#0a1424; --indigo:#0f1c30; --indigo-2:#182840;
  --accent:#8fbfe6; --accent-soft:#c2e0f5; --rose:#7c8fd4; --dawn:#5fa8c4;
  --cream:#eaf1f8; --muted:rgba(234,241,248,.56);
  --faint:rgba(234,241,248,.14); --line:rgba(234,241,248,.10);
  --display:"Fraunces",serif; --body:"Spline Sans",system-ui,sans-serif;
  --mono:"Spline Sans Mono",monospace; --ease:cubic-bezier(.16,1,.3,1);
}
/* rgb triples for rgba() gradients & canvas:
   accent 143,191,230 · cyan 95,168,196 · periwinkle 124,143,212 · text 234,241,248 */
```

**Reference implementation:** [`index.html`](index.html) in this directory (the Meridian
observatory landing page) is the canonical, complete realization of this contract. This
directory is a standalone style — the contract and its reference implementation live here
together.
