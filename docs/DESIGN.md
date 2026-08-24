# Design Guidelines

This document covers the visual system for the West Lafayette Shuttle Timetable. All design decisions are implemented in the `<style>` block of `index.html`.

## Color tokens

All colors are defined as CSS custom properties in `:root`. Use these everywhere — never hardcode hex values in rules.

| Token | Light value | Usage |
|---|---|---|
| `--reindeer` | `#1a6b9a` | Reindeer Shuttle accent — badges, book buttons (fixed across themes) |
| `--reindeer-light` | `#e8f3fa` | Reindeer badge background (fixed across themes) |
| `--limo` | `#c0562a` | Lafayette Limo accent — badges, book buttons (fixed across themes) |
| `--limo-light` | `#fdf0ea` | Lafayette Limo badge background (fixed across themes) |
| `--bg` | `#f7f8fa` | Page background |
| `--card` | `#ffffff` | Table and info card background |
| `--border` | `#e2e5ea` | All borders and dividers |
| `--text` | `#1c2230` | Body text |
| `--muted` | `#6b7280` | Secondary text, table headers, footnotes |
| `--heading` | `#0f172a` | Primary headings, large time numbers |
| `--surface-alt` | `#f1f5f9` | Table header background |
| `--row-hover` | `#f8fafc` | Table row hover background |
| `--note-bg` / `--note-border` / `--note-text` | `#fffbeb` / `#fcd34d` / `#92400e` | Note bar callout |
| `--footer-bg` | `#0f172a` | Footer background (fixed across themes, matches the always-dark hero) |
| `--offset` / `--offset-bg` | `#8a5a00` / `#fdf3df` | "+15m"-style stop-offset badge in provider cards |

### Dark mode

The page follows the system color scheme via `@media (prefers-color-scheme: dark)` — there is no manual toggle. The media query overrides `--bg`, `--card`, `--border`, `--text`, `--muted`, `--heading`, `--surface-alt`, `--row-hover`, `--note-bg`, `--note-border`, `--note-text`, `--offset`, and `--offset-bg` with dark-mode-safe values (all pairings verified ≥ 4.5:1 contrast). The hero banner, main tab bar, and footer stay a fixed dark navy in both themes — they don't reference the overridden tokens. Provider accent tokens (`--reindeer`, `--limo`, and their `-light` variants) are also fixed across themes since their badge/button pairings already meet contrast in both.

## Typography

| Element | Size | Weight | Notes |
|---|---|---|---|
| Page title (hero) | 22px | 800 | |
| Tab button | 15px | 700 | |
| Table column heading (above each side-by-side table) | 13px | 800 | Uppercase, 0.4px letter-spacing |
| Table header (`th`) | 11px | 700 | Uppercase, 0.6px letter-spacing |
| Time (big) | 14px | 700 | `--heading` color |
| Timezone label | 10.5px | 500 | `--muted` color, inline after time |
| Arrival time | 13px | 600 | |
| Provider card stop sequence | 12.5px | 400 | `--text` color |
| Stop offset badge (e.g. "+15m") | 10px | 700 | `--offset` on `--offset-bg` |
| Caveat line (unpublished per-stop times) | 10.5px | 400 italic | `--muted` color |
| Trip duration line | 11px | 700 | `--muted` color |
| Provider card meta (fare, pickup/drop-off) | 12px | 400 | `--muted` color, `<strong>` in `--heading` |

System font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`

## Layout

- Max content width: **1080px**, centered with `margin: 0 auto`
- Content padding: **24px top/bottom, 16px left/right**
- Side-by-side tables: `.tables-row` is a two-column CSS grid, 16px gap, one direction's table per column
- Provider cards: `.provider-grid`, CSS grid `repeat(auto-fit, minmax(280px, 1fr))`, 12px gap
- Tables: full width within their grid column, `border-collapse: collapse`, 10px border-radius with `overflow: hidden`, wrapped in `.table-scroll` (`overflow-x: auto`) in case a very narrow viewport still needs to scroll

## Components

### Provider badge
```html
<span class="provider-badge badge-reindeer">Reindeer</span>
<span class="provider-badge badge-limo">Lafayette Limo</span>
```
11px, 700 weight, 3px/7px padding, 4px radius.

### Book button
```html
<a class="book-link book-reindeer" href="...">Book online</a>
<a class="book-link book-limo" href="...">Book online</a>
```
12px, 600 weight, 5px/11px padding, 5px radius. Uses provider accent color as background. One per provider card (not one per table row).

### Note bar (yellow callout)
```html
<div class="note-bar">⏰ ...</div>
```
Used once per airport tab, above the pair of tables, to explain timezone context. Background `#fffbeb`, border `#fcd34d`, text `#92400e`.

### Provider reference card
```html
<div class="provider-card">
  <h4>🦌 Reindeer Shuttle</h4>
  <div class="route-block">
    <span class="dir-label">Purdue → ORD</span>
    <div class="stops">Quality Inn → Co-Rec Circle<span class="off">+15m</span> → PMU<span class="off">+30m</span></div>
    <div class="trip-dur">⏱ Trip duration: 3h30–3h45m</div>
  </div>
  <div class="route-block">...second direction...</div>
  <div class="card-meta">fare, pickup/drop-off details</div>
  <div class="book-row"><a class="book-link ...">Book online</a> <span class="phone">📞 ...</span></div>
</div>
```
One card per provider, shared by both directions of that airport tab (not split per direction). Each `.route-block` holds that direction's ordered stop sequence, with `.off` badges for stops where the provider publishes a fixed offset from departure, and a `.caveat` line instead when they only publish one arrival window for a cluster of stops. `.trip-dur` states the (possibly ranged) duration once per direction, since it's constant across every run of that provider+direction.

### Tab system
- **Main tabs** (ORD / IND): dark bar (`#1e293b`), active tab has blue bottom border (`#60a5fa`). These are the only tabs — direction is no longer tab-switched, both directions render as side-by-side tables.

## Accessibility

- Maintain color contrast ≥ 4.5:1 for all text/background pairs
- Buttons use `<button>` elements (keyboard focusable)
- Book links open in `target="_blank"` — acceptable for external booking sites
- On narrow viewports (<650px), the side-by-side tables and the provider-card grid stack to a single column instead of hiding any data

## Responsiveness

The layout is mobile-friendly by default (fluid widths, wrapping flex). The one explicit breakpoint at **650px** stacks `.tables-row` and reduces tab button padding; `.provider-grid`'s `auto-fit` already reflows without a breakpoint.
