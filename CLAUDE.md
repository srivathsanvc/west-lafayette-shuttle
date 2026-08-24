# CLAUDE.md — West Lafayette Shuttle Timetable

This file tells Claude (or any AI assistant) how to work with this codebase.

## What this project is

A single-file static website (`index.html`) that combines airport shuttle schedules for West Lafayette, Indiana from two providers:
- **Reindeer Shuttle** — serves ORD and IND routes
- **Lafayette Limo** — serves ORD and IND routes

The page uses tabbed navigation (ORD / IND, then inbound / outbound within each) to keep it readable. Hosted on GitHub Pages at `https://srivathsanvc.github.io/west-lafayette-shuttle`.

## File structure

```
index.html          ← entire site lives here (HTML + CSS + JS, no build step)
README.md
CONTRIBUTING.md
CLAUDE.md           ← this file
LICENSE
docs/
  DESIGN.md         ← color tokens, typography, component patterns
.github/
  ISSUE_TEMPLATE/   ← schedule-update.md, bug-report.md
  PULL_REQUEST_TEMPLATE.md
```

## Key conventions

### HTML structure
- Main tabs: `#panel-ord` and `#panel-ind` (toggled by `switchTab()`) — these are the only tabs; direction is not tab-switched
- Each airport tab holds two tables side by side (`.tables-row`), IDs `{airport}-to-wl` and `{airport}-to-{airport}`, plus a "Provider reference" section below (`.provider-grid`) with one card per provider covering both directions
- Each shuttle departure = one `<tr>` inside a `<tbody>`, columns `Provider | Departs | Arrives` only — stops, fare, and the book link live once per provider in that provider's reference card, not per row
- Rows must stay sorted by departure time (earliest first), with providers interleaved chronologically rather than grouped

### CSS
- All colors are CSS variables defined in `:root` — never use hardcoded hex values in rules
- Reindeer Shuttle color: `--reindeer` (#1a6b9a) with `--reindeer-light` for badge backgrounds
- Lafayette Limo color: `--limo` (#c0562a) with `--limo-light` for badge backgrounds
- See `docs/DESIGN.md` for the full token list and component patterns

### Timezone handling
- West Lafayette / IND = **Eastern Time (ET)**
- Chicago / ORD = **Central Time (CT)**, which is 1 hour behind ET
- Always label times with their timezone in the ORD tables; IND tables can omit since both endpoints are ET

### Data integrity rules
- Never invent or extrapolate schedule times — only use times sourced directly from the providers' websites
- Always include the source URL when updating schedule data (in PR description or commit message)
- Pricing shown is the online fare; walk-up/cash fares are in the info cards, not the table rows

## Common tasks

### Add a new departure row
Find the right `<tbody>` by section ID, insert a `<tr>` in time order, follow the column pattern:
`Provider badge | Depart time + TZ | Arrive time`
No stops/fare/book cells — those aren't repeated per row. If the new departure's stop sequence or duration differs from that provider's existing rows, update the matching `.route-block` in its provider card too.

### Update a fare
Find the provider's `.provider-card` (`.card-meta`) in the relevant airport tab and update the dollar amount there — fares live once per provider, not per row.

### Change the tab color scheme
Edit the `.tab-btn.ord-tab` / `.tab-btn.ind-tab` rules and update the corresponding CSS variables. Keep contrast ratio ≥ 4.5:1 for text on colored backgrounds.

## What not to do

- Don't split the site into multiple files (CSS, JS) — the single-file constraint is intentional for GitHub Pages simplicity
- Don't add JavaScript frameworks or npm dependencies
- Don't guess schedule times — only transcribe from official provider pages
- Don't change pricing without verifying on the provider's site first
