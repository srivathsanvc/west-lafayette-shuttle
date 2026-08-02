# Design Guidelines

This document covers the visual system for the West Lafayette Shuttle Timetable. All design decisions are implemented in the `<style>` block of `index.html`.

## Color tokens

All colors are defined as CSS custom properties in `:root`. Use these everywhere — never hardcode hex values in rules.

| Token | Value | Usage |
|---|---|---|
| `--reindeer` | `#1a6b9a` | Reindeer Shuttle accent — badges, book buttons |
| `--reindeer-light` | `#e8f3fa` | Reindeer badge background |
| `--limo` | `#c0562a` | Lafayette Limo accent — badges, book buttons |
| `--limo-light` | `#fdf0ea` | Lafayette Limo badge background |
| `--bg` | `#f7f8fa` | Page background |
| `--card` | `#ffffff` | Table and info card background |
| `--border` | `#e2e5ea` | All borders and dividers |
| `--text` | `#1c2230` | Body text |
| `--muted` | `#6b7280` | Secondary text, table headers, footnotes |
| `--heading` | `#0f172a` | Primary headings, large time numbers |

## Typography

| Element | Size | Weight | Notes |
|---|---|---|---|
| Page title (hero) | 22px | 800 | |
| Tab button | 15px | 700 | |
| Sub-tab button | 13px | 600 | |
| Table header | 11px | 700 | Uppercase, 0.6px letter-spacing |
| Time (big) | 16px | 700 | `--heading` color |
| Timezone label | 11px | 500 | `--muted` color, inline after time |
| Arrival time | 14px | 600 | |
| Stop descriptions | 12px | 400 | `--muted` color |
| Price | 14px | 700 | `--heading` color |
| Price note | 11px | 400 | `--muted` color |
| Info card body | 12px | 400 | `--muted` color |
| Footnotes | 11px | 400 | `--muted` color |

System font stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`

## Layout

- Max content width: **1000px**, centered with `margin: 0 auto`
- Content padding: **24px top/bottom, 16px left/right**
- Info cards: CSS grid, `repeat(auto-fit, minmax(240px, 1fr))`, 12px gap
- Tables: full width, `border-collapse: collapse`, 10px border-radius with `overflow: hidden`

## Components

### Provider badge
```html
<span class="provider-badge badge-reindeer">Reindeer</span>
<span class="provider-badge badge-limo">Lafayette Limo</span>
```
11px, 700 weight, 3px/7px padding, 4px radius.

### Book button
```html
<a class="book-link book-reindeer" href="...">Book</a>
<a class="book-link book-limo" href="...">Book</a>
```
12px, 600 weight, 5px/11px padding, 5px radius. Uses provider accent color as background.

### Note bar (yellow callout)
```html
<div class="note-bar">⏰ ...</div>
```
Used above each timetable to explain timezone context. Background `#fffbeb`, border `#fcd34d`, text `#92400e`.

### Info card
```html
<div class="info-card">
  <h4>🦌 Reindeer Shuttle — ORD</h4>
  <ul>...</ul>
</div>
```
White background, `--border` border, 10px radius, 14px/16px padding.

### Tab system
- **Main tabs** (ORD / IND): dark bar (`#1e293b`), active tab has blue bottom border (`#60a5fa`)
- **Sub-tabs** (direction): light bar (`#f1f5f9`), active has dark bottom border

## Accessibility

- Maintain color contrast ≥ 4.5:1 for all text/background pairs
- Buttons use `<button>` elements (keyboard focusable)
- Book links open in `target="_blank"` — acceptable for external booking sites
- On narrow viewports (<650px), the stops column is hidden via CSS to keep the table readable

## Responsiveness

The layout is mobile-friendly by default (fluid widths, wrapping flex). The one explicit breakpoint at **650px** hides the stops column in tables to keep departure and arrival times visible on small screens.
