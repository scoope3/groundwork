# feed

Indicator files written by the publisher. Columns are described in `METHOD.md`.

* `YYYY-MM-DD.csv`, `.stix2.json`, `.misp.json`: what was FIRST published on that day, and nothing else. A day with nothing new has no files. An indicator of a case appears in at most one day file, the one for the day it was first published, so reading every day file never gives one twice. On its own day a file can still change (a same-day correction); after that it is fixed.
* `rolling-30d.csv`: every indicator published now that was first published in the last 30 days, with its current evidence types and first-finder answer. Corrections and retractions show here at the next publication. An indicator withdrawn and published again more than 30 days after its first publication is not listed here; it is in the case's own list.
* For the full current list of a case, at any age, read `cases/<case>/indicators.csv`.

Until 2026-11-21 a day file was a full snapshot; the file for 2026-11-20 is both.
