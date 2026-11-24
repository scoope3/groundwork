# feed

Indicator files written by the publisher. Columns are described in `METHOD.md`.

* The day files `YYYY-MM-DD.csv`, `.stix2.json` and `.misp.json` hold what was first published on that day and nothing else. A day on which nothing new was published has no day files at all. An indicator of a case appears in at most one day file, the one for the day it was first published, so reading every day file never gives one twice. On its own day a file can still change with a same-day correction. After that day a file is normally left alone, and every later rewrite of a day file is listed in `CHANGELOG.md`.
* The file `rolling-30d.csv` lists every indicator published now that was first published in the last 30 days, with its current evidence types. Corrections and retractions show up in this file at the next publication. An indicator withdrawn and published again more than 30 days after its first publication is not listed here, but it stays in the case's own list.
* For the full current list of a case, at any age, read `cases/<case>/indicators.csv`.

Until 2026-11-21 a day file was a full snapshot; the file for 2026-11-20 is both.

Every day file published in the old layout was rewritten once for the layout change recorded in `CHANGELOG.md`, and no row was added to or removed from them.
