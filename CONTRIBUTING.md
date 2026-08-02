# Contributing

Thanks for helping keep this timetable accurate! The most common contribution is a **schedule update** when Reindeer Shuttle or Lafayette Limo changes their times or prices.

## Updating a schedule

1. **Verify the new schedule** on the provider's website:
   - Reindeer Shuttle: https://www.reindeershuttle.com/
   - Lafayette Limo (IND): https://lafayettelimo.com/services/indianapolis-airport-shuttle-service
   - Lafayette Limo (ORD): https://lafayettelimo.com/services/ohare-airport-shuttle-service

2. **Open `index.html`** and find the relevant `<table>` section. Tables are organized in this order inside the file:
   - ORD → West Lafayette (`id="ord-to-wl"`)
   - West Lafayette → ORD (`id="ord-to-ord"`)
   - IND → West Lafayette (`id="ind-to-wl"`)
   - West Lafayette → IND (`id="ind-to-ind"`)

3. **Edit the `<tbody>` rows.** Each shuttle departure is one `<tr>`. The column order is:
   `Provider | Departs | Stops | Arrives | Fare | Book`

4. **Keep rows sorted by departure time** within each table (earliest at top).

5. **Update pricing** in the info cards near the top of each tab panel if fares changed.

6. **Test locally** before submitting — open `index.html` in a browser and click through all four tab combinations.

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
