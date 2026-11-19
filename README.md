# MARÉE — A House at the Edge of the Sea

A bright, restrained editorial photography single-file website for **MARÉE** (French for *tide*), a coastal house at the edge of the sea. Built with native HTML, CSS, and JavaScript — zero frameworks, zero external requests, and all four photographs inlined as base64 data URIs (`index.html`, ~842 KB).

---

## Design & Motion Craft

- **Persistent Editorial Chrome**
  - **14px Inset Frame Border**: A fixed `1px` semi-transparent hairline frame wraps the viewport (`pointer-events: none`) with safe inner padding across all chapters.
  - **Adaptive Top Navigation & Bottom Folio Bar**: Centered hairline-underline navigation (`Journal / The House / Visit`), geometric asterisk brand mark (`✳ Marée`), pill CTA (`Plan a visit ↗`), and fixed bottom bar (`SCROLL TO EXPLORE ↓` · `LIVE AT SEA` · `01 / 04 → 04 / 04`). Chrome ink smoothly switches between deep slate ink (`#16303a`) and warm ivory (`#f6f3ec`) as the viewer moves from sunlit sky to underwater chapters and back to cream paper.
  - **Subtle Film Grain Overlay**: Inline SVG `feTurbulence` fractal noise at `opacity: 0.036` (≤ 0.05) for subtle photographic texture.

- **01 · Sea Surface (`#surface`)**
  - Full-bleed golden sunset wave (`hero.jpg`) with a slow 20-second `ease-out` Ken Burns push (`scale(1 → 1.08)`) and a gentle sunlit upper-left sky veil (no dark vignette).
  - Staggered on-load headline reveal (`translateY`, `opacity`, and subtle `blur` clearing at `120ms` intervals) for *Drift a little / closer.* (`clamp(3.5rem, 9vw, 8.5rem)`).
  - Differentiated mouse micro-parallax (`≤ 10px`) between photograph and typography smoothed via `requestAnimationFrame` + linear interpolation (`lerp`).

- **02 · Scroll-Driven Dive Transition (`#dive`)**
  - `260vh` scroll runway with an inner `position: sticky; height: 100vh` stage — zero scroll hijacking.
  - Smoothed scroll progress `p ∈ [0, 1]` drives a continuous submersion: the sunset surface layer (`hero.jpg`, reused from the embedded hero URI to avoid duplicating base64 payload) fades from `opacity: 1 → 0` while pushing forward, revealing `dive.jpg` settling from `scale(1.15) → scale(1.0)`.
  - A soft top-down sunbeam gradient swells mid-dive (`sin(p · π)`) and subsides; centered italic serif copy (*Then the surface closes above you.*) fades in around `p ≈ 0.45` and fades out around `p ≈ 0.80`.

- **03 · The Shallows (`#shallows`)**
  - Full-bleed sunlit underwater chapter (`min-height: 112vh`) with vertical scroll parallax (`translateY(-6% → +6%)`) smoothed by `rAF + lerp`.
  - Restrained `<canvas>` underwater motes (34 soft specks) drifting slowly upward.
  - Bottom-left editorial typography (*Light, doing its / slow work.*), two-sentence prose, and a quiet hairline print-style `FIELD NOTES` row (`DEPTH — 12 M · LIGHT — 78% · WATER — 21°C`) — purely typographic, no HUD panels.

- **04 · Inland Interlude (`#moss`)**
  - Warm ivory paper ground (`#f4f1ea`) with deep ink (`#16303a`) typography.
  - Asymmetric editorial grid: left copy column paired with a `52%`-wide, `78vh`-tall moss photograph on the right, revealed via `clip-path` and gentle internal glide.
  - Oversized serif headline (*The forest keeps / its own tide.*) overlaps the left edge of `moss.jpg` by ~15%. A `ResizeObserver`-synchronized twin headline clipped inside the photo container cleanly flips overlapping letterforms from deep ink (`#16303a`) to warm ivory (`#f4f1ea`) along the exact edge of the photograph (both horizontally on desktop and vertically along the bottom photo edge on mobile).

- **05 · Finale & Colophon (`#visit`)**
  - Full-viewport quiet coastal mist closing page (`#f4f1ea → #ebf0ef`) with centered display serif (*The sea, at eye level.*), `Back to the surface ↑` smooth-scroll pill button, and minimal hairline colophon (`© 2026 Marée` · `Photography — Pexels` · `47.6° N, 122.3° W`).

- **Accessibility & Responsiveness**
  - Native system serif (`"Playfair Display", "Iowan Old Style", Georgia, "Noto Serif", "Times New Roman", serif`) and sans-serif stacks — no external font requests.
  - Responsive mobile layout (`≤ 860px`): fluid `clamp()` display scale with zero horizontal overflow, stacked Moss chapter with bottom-edge title overlap, and simplified bottom folio bar (`SCROLL ↓` + chapter number).
  - Honors `prefers-reduced-motion: reduce`: disables Ken Burns zoom, mouse/scroll parallax, reveal transitions, and floating motes.

---

## Asset Sources

All photographs are sourced from **Pexels** and embedded directly into `index.html` as `data:image/jpeg;base64,...` URIs:

| Asset | Dimensions | Raw Size | Role |
| --- | --- | --- | --- |
| `assets/hero.jpg` | 1600 × 1067 | 145.5 KB | Chapter 01 full-bleed sunset surface & Dive surface continuity layer |
| `assets/dive.jpg` | 1600 × 1200 | 190.5 KB | Chapter 02 half-surface / underwater submersion transition |
| `assets/shallows.jpg` | 1600 × 900 | 160.0 KB | Chapter 03 sunlit shallow seagrass & reef chapter |
| `assets/moss.jpg` | 1600 × 1058 | 111.1 KB | Chapter 04 warm ivory inland moss interlude |

---

## Verification Screenshots

Headless Chromium captures at `1440 × 900` verifying layout, contrast, overlap registration, chapter counter progression, zero console errors, and zero external requests:

- `shot-hero.png` — Chapter `01 / 04` surface hero
- `shot-dive.png` — Chapter `02 / 04` mid-dive submersion transition
- `shot-shallows.png` — Chapter `03 / 04` sunlit shallows & field notes
- `shot-moss.png` — Chapter `04 / 04` warm ivory moss interlude with dual-tone edge overlap
- `shot-finale.png` — Closing folio & minimal colophon
