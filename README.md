# MegaDevCourse — S01E03 "what it shows"

Re-reading support ticket **#4471**. The desk merged **412** reports about wrong dates into one
ticket and marked it *known* — one bug, one fix queued. Running the knowledge base's own cause
logic over the export shows the one ticket is really **three distinct bugs**.

## Tickets filed (one per problem, with the reports each covers)

| Issue | Problem | Reports | State |
|---|---|---|---|
| [#1](https://github.com/BartCodeDev/MegaDevCourse/issues/1) | Date parser reads month-first → day-first tenants' dates flip by a month | 379 | closed · completed (the desk shipped the parser fix) |
| [#2](https://github.com/BartCodeDev/MegaDevCourse/issues/2) | booking-v3 form hint (`MM/DD/YYYY`) misleads day-first users | 33 | closed · not planned (separate bug, not in the parser fix) |
| [#3](https://github.com/BartCodeDev/MegaDevCourse/issues/3) | Dates off by one day (timezone / day-boundary), not by a month | 5 | open (unconfirmed; needs a timezone / DST check) |

Counted as the kb's own view (`CauseTable`) counts: one id = one report (the export lists some twice),
cause from the tenant's locale and booking form (`causes.ts`). The two causes are 379 + 33 = 412. The 5
one-day reports are a subset of the `parser` row, taken out for their own ticket (#3) because a month
swap cannot move a date by one day.

## The knowledge base

[`support-kb/`](support-kb/) is the support desk's kb export. The work adds one page, in two forms:

- the source: [`support-kb/src/routes/kb/incidents/4471-what-it-shows/+page.svx`](support-kb/src/routes/kb/incidents/4471-what-it-shows/+page.svx) — uses the kb's own `CauseTable` and `QueueTimeline` (numbers computed from the data at render time) and is signed, per the kb's conventions;
- the page as the desk will see it: [`rendered/4471-what-it-shows.html`](rendered/4471-what-it-shows.html) — a static copy, no scripts.

The split is computed, not guessed: `causeOf()` in `support-kb/src/lib/kb/causes.ts` returns `parser` or
`hint` from each tenant's locale and booking form; the 5 one-day reports are the desk's own `oneDayMove`
list in `support-kb/src/lib/data/desk-notes.json`.
