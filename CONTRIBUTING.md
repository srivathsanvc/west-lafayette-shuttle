# Contributing

Thanks for helping keep this timetable accurate! The most common contribution is a **schedule update** when Reindeer Shuttle or Lafayette Limo changes their times or prices.

## Updating a schedule

1. **Verify the new schedule** on the provider's website:
   - Reindeer Shuttle: https://www.reindeershuttle.com/
   - Lafayette Limo (IND): https://lafayettelimo.com/services/indianapolis-airport-shuttle-service
   - Lafayette Limo (ORD): https://lafayettelimo.com/services/ohare-airport-shuttle-service

2. **Open `index.html`** and find the relevant `<table>` section. Each airport tab (`#panel-ord`, `#panel-ind`) holds two tables side by side:
   - ORD → Purdue (`id="ord-to-wl"`) / Purdue → ORD (`id="ord-to-ord"`)
   - IND → Purdue (`id="ind-to-wl"`) / Purdue → IND (`id="ind-to-ind"`)

3. **Edit the `<tbody>` rows.** Each shuttle departure is one `<tr>`. The column order is:
   `Provider | Departs | Arrives`

   Stops, fare, and the book link are **not** repeated per row — they live once per provider in the "Provider reference" card below the two tables (one card covers both directions). If you're adding or removing a departure, only the table row changes; if the stop sequence, duration, or fare itself changed, update that provider's card too.

4. **Keep rows sorted by departure time** within each table (earliest at top), interleaving providers chronologically rather than grouping by provider.

5. **Update pricing, stops, or duration** in the relevant provider card's `.route-block` / `.card-meta`, not in the table rows.

6. **Test locally** before submitting — open `index.html` in a browser and click through both airport tabs.

7. **Open a PR** with a title like `Update Reindeer IND schedule – Aug 2026` and link to the source page you used.

## Reporting a schedule error

Open an issue using the **Schedule Update** template and include:
- Which route is wrong
- What the page currently shows
- What it should show
- Link to the provider's schedule page as source

## Design changes

See [docs/DESIGN.md](docs/DESIGN.md) before making visual changes. Keep PRs focused — schedule updates and design changes should be separate PRs.

## Code style

- All markup, styles, and scripts stay in `index.html` (no separate files)
- Use CSS variables defined in `:root` for all colors — no hardcoded hex values in rules
- Keep the JS minimal; no frameworks or libraries
- Run a quick a11y check (tab navigation, color contrast) before submitting UI changes
