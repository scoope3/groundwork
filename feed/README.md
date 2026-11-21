# feed

Indicator files written by the publisher. Columns are described in `METHOD.md`.

* `YYYY-MM-DD.csv`, `.stix2.json`, `.misp.json`: what was FIRST published on that day, and nothing else. A day with nothing new has no files. Each indicator of a case appears in exactly one day file, so reading every day file gives each one once.
* `rolling-30d.csv`: every indicator published now that was first published in the last 30 days, with its current evidence types and first-finder answer. Corrections and retractions show here at the next publication.
* For the full current list of a case, at any age, read `cases/<case>/indicators.csv`.

Until 2026-11-21 a day file was a full snapshot; the file for 2026-11-20 is both.
