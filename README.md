# MegaDevCourse — S01E03 "what it shows"

Re-reading support ticket **#4471**. The desk merged **412** reports about wrong dates into one
ticket and marked it *known* — one bug, one fix queued. Running the knowledge base's own cause
logic over the export shows the one ticket is really **three distinct bugs**.

## Tickets filed (one per problem, with the reports each covers)

| Issue | Problem | Reports |
|---|---|---|
| [#1](https://github.com/BartCodeDev/MegaDevCourse/issues/1) | Date parser reads month-first → day-first tenants' dates flip by a month | 374 |
| [#2](https://github.com/BartCodeDev/MegaDevCourse/issues/2) | booking-v3 form hint (`MM/DD/YYYY`) misleads day-first users | 33 |
| [#3](https://github.com/BartCodeDev/MegaDevCourse/issues/3) | Dates off by one day (timezone / day-boundary), not by a month | 5 |

374 + 33 + 5 = 412.

## The knowledge base

[`support-kb/`](support-kb/) is the support desk's kb export. The page added for this work is
[`support-kb/src/routes/kb/incidents/4471-what-it-shows/+page.svx`](support-kb/src/routes/kb/incidents/4471-what-it-shows/+page.svx):
it uses the kb's own `CauseTable` and `QueueTimeline` components (numbers computed from the data at
render time) and is signed, per the kb's conventions.

The split is computed, not guessed: `causeOf()` in `support-kb/src/lib/kb/causes.ts` returns
`parser` or `hint` from each tenant's locale and booking form; the 5 one-day reports are the desk's
own `oneDayMove` list in `support-kb/src/lib/data/desk-notes.json`.
