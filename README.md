# West Lafayette Shuttle Timetable

A single-page, tabbed reference combining shuttle schedules from **Reindeer Shuttle** and **Lafayette Limo** for trips between West Lafayette / Purdue University and Chicago O'Hare (ORD) or Indianapolis (IND) airports.

**Live site → [srivathsanvc.github.io/west-lafayette-shuttle](https://srivathsanvc.github.io/west-lafayette-shuttle)**

---

## What's in it

- Combined schedules for both providers, sorted by departure time
- Separate tabs for ORD and IND routes, with sub-tabs for each direction
- Pricing, key pickup stops, and direct booking links
- Timezone callouts (ORD/Chicago = CT; WL/IND = ET)

## Data sources

| Provider | Route | Schedule page |
|---|---|---|
| Reindeer Shuttle | ORD ↔ Purdue, IND ↔ Purdue | [reindeershuttle.com](https://www.reindeershuttle.com/) |
| Lafayette Limo | ORD ↔ West Lafayette | [lafayettelimo.com/services/ohare-airport-shuttle-service](https://lafayettelimo.com/services/ohare-airport-shuttle-service) |
| Lafayette Limo | IND ↔ West Lafayette | [lafayettelimo.com/services/indianapolis-airport-shuttle-service](https://lafayettelimo.com/services/indianapolis-airport-shuttle-service) |

> **Always verify schedules on the providers' websites before booking.** Schedules and prices change seasonally.

## Keeping it current

When schedules change, edit `index.html` directly — all timetable data lives in the HTML tables in that file. See [CONTRIBUTING.md](CONTRIBUTING.md) for the step-by-step update process.

## Tech stack

Plain HTML + CSS + vanilla JS. No build step, no dependencies, no framework. The entire site is `index.html`.

## Local preview

```bash
# Any of these work
open index.html
python3 -m http.server 8080
npx serve .
```

## License

MIT — see [LICENSE](LICENSE).
