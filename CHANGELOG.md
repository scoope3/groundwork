# Corrections log

Dated record of every retraction, re-grading or correction to a published case or feed entry. Newest first.

## 2026-11-21

* **Feed, duplicates.** The day file for 2026-11-21 repeated all 125 indicators of 2026-11-20, and `rolling-30d.csv` listed those 125 twice, for about half an hour after 00:00 UTC. Both were replaced the same day. From this date a day file holds only what was first published that day, and the rolling file is the current list of what was first published in the last 30 days. `feed/README.md` and `METHOD.md` now say so.
* **Feed, STIX ids.** Indicator ids in the STIX files were different on every run. They are now stable (UUIDv5 of type, value and case). Ids in the 2026-11-20 file were not changed.
* **Case `windows-defender-cc-lure-repos`, scope narrowed and case extended.** The title and summary said the lure repos deliver the analysed stealer. That was shown only for the download chain that was run (`devtools8[.]lol` with `toolget2[.]lol`, and `quickrun31[.]cc`); for the other delivery hosts the payload was never retrieved. The text now says so. Added the same day: four delivery hosts, a second build's server, page and contract, three file hashes and 241 lure repositories found by a second crawl.

The first case was published on 2026-11-20.
