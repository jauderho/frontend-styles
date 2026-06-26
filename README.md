# frontend-styles

Four self-contained design languages, each committing to a single idea and following
it without compromise. Every theme is a standalone, zero-build `index.html` with an
inline `<style>` block, a binding `AESTHETIC_CONTRACT.md`, and a live reference page.

**Live site → <https://jauderho.github.io/frontend-styles/>**

A curated gallery of all four lives at the repo root — open it
[live](https://jauderho.github.io/frontend-styles/) or locally via
[`index.html`](index.html).

```
catfu        cassette-futurism — a machined instrument panel
cyberdeck    deep-space telemetry — mission control
meridian     cinematic dark-luxury — descending into the dark
quiet-gilt   restrained heirloom-ledger — quiet wealth
```

All four share a common floor: **dark-first with a light/dark toggle**, WCAG AA
contrast verified in both themes, full keyboard operability, `prefers-reduced-motion`
honored, and no chart libraries — every data visualization is hand-built CSS/SVG.

---

## Design Language

### catfu — cassette-futurism

> *Reference page: the cobalt **cm-1 field sampler**.*

A machined instrument panel realized in software. The governing mental model is a
physical device: every pixel is a function, a label, a lit display, or a control.
The discipline is total — **zero border-radius** on structure (enclosures are
machined, not molded), **no drop shadows or gradient fills** (matte polycarbonate
and phosphor screens have neither), and **mechanical motion only** (`steps()`
easing, 50–80ms snaps, blink as the primary animation — never an eased curve).

| | |
|---|---|
| **Accent** | Cobalt blue `#2e7dc4`, sampled pixel-for-pixel from a real device |
| **Type** | Archivo / Archivo Expanded (display), IBM Plex Mono (body), Press Start 2P (LCD accent) |
| **Feel** | Dense, functional, tactile — information density as a feature |

→ [view live](https://jauderho.github.io/frontend-styles/catfu/) · [contract](catfu/AESTHETIC_CONTRACT.md)

---

### cyberdeck — deep-space telemetry

> *Reference page: **mission control for self-hosted infrastructure**.*

A deep-space navy canvas with data rendered like telemetry — dense, precise, calm
under load. The screen should read as a piece of equipment, not a brochure. The
identity is a strict **two-voice type split**: a humanist sans (Outfit) carries
everything operational, while a monospace (JetBrains Mono) is reserved for anything
*literal* — file paths, IDs, destinations, commands, code.

| | |
|---|---|
| **Accent** | Sky/cyan `#38bdf8` (structural) + a semantic spectrum |
| **Type** | Outfit (chrome/UI/numbers), JetBrains Mono (literal data only) |
| **Feel** | Telemetry-grade, dense but calm; glow used sparingly |

→ [view live](https://jauderho.github.io/frontend-styles/cyberdeck/) · [contract](cyberdeck/AESTHETIC_CONTRACT.md)

---

### meridian — cinematic dark-luxury

> *Reference page: **a private observatory in the high desert**.*

Built around a single idea: **descending into the dark.** The canonical *Celestine*
palette is a glacial, near-monochrome winter night — deep slate-blue grounds, a cold
ice-blue accent, moonlit white type. The emotional target is **quiet awe**: standing
under a sky dark enough that the Milky Way is loud.

| | |
|---|---|
| **Accent** | Cold ice-blue `#8fbfe6` (moonlight), rationed |
| **Type** | Fraunces (serif voice), humanist grotesque (body), mono (labels) |
| **Feel** | Cinematic, editorial, contemplative; atmosphere over flat fills |

→ [view live](https://jauderho.github.io/frontend-styles/meridian/) · [contract](meridian/AESTHETIC_CONTRACT.md)

---

### quiet-gilt — restrained heirloom-ledger

> *Reference page: **a private wealth house**.*

Calm, confident, quiet — an heirloom-ledger feel, not a fintech dashboard. **One gold
accent**, used sparingly, earns its weight; semantic green/red/amber exist only for
meaning, never decoration. Typography does the work: Newsreader serif gives headlines
and hero numbers their voice, Hanken Grotesk carries the UI, and hierarchy comes from
size, weight, and whitespace rather than boxes and borders. **No monospace anywhere** —
aligned numbers use tabular figures on the sans face.

| | |
|---|---|
| **Accent** | Gold `#d4b87a` (dark) / `#9a7b2e` (light) — the one accent |
| **Type** | Newsreader (serif headings/numbers), Hanken Grotesk (UI) |
| **Feel** | Restrained, premium, quiet; the answer first |

→ [view live](https://jauderho.github.io/frontend-styles/quiet-gilt/) · [contract](quiet-gilt/AESTHETIC_CONTRACT.md)

---

## Repository layout

```
.
├── index.html              # curated gallery linking to all four themes
├── catfu/                  # cassette-futurism
├── cyberdeck/              # deep-space telemetry
├── meridian/               # cinematic dark-luxury
├── quiet-gilt/             # restrained heirloom-ledger
```

Each theme directory contains its own `index.html` (the reference implementation) and
`AESTHETIC_CONTRACT.md` (the binding design contract). When the contract and the code
disagree, that's a bug to flag — not a choice to make silently.

## Running locally

Every page is a single self-contained HTML file; just open one in a browser. To serve
the whole gallery:

```bash
python3 -m http.server 8731
# then visit http://localhost:8731
```
