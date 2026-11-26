# Corrections log

Dated record of every retraction, re-grading or correction to a published case or feed entry. Newest first.

## 2026-11-26

* **Feed and case lists, layout change.** Case `indicators.csv` files gained two columns, `source` and `source_detail`, described under "Source" in `METHOD.md`. Day CSV files gained `role`, `linked_to` and `source`, and `rolling-30d.csv` gained `role`, `description`, `linked_to`, `source` and `details`. Every day CSV file published before this change was rewritten once to add its three columns, with no row added or removed, and the STIX and MISP day files were not changed. `files.csv` gained `kind`, `delivered_by` and `source`, each filled only where recorded. The layout change itself added, withdrew or re-graded no indicator, and indicators added on the same day are listed in the next entry.
* **Case `windows-defender-cc-lure-repos`, two hosts added.** `pkgload2.tools` was added as a delivery host, and it is named in a macOS command in lure READMEs that also carry the Windows command for `pkgsetup.cc`. The script at that address was retrieved once, and it is written to download an archive from the same host. The archive was not retrieved, so what it installs is not known. `toolget2.lol`, already listed as a next-stage host, is now also listed as a delivery host, because one lure README names it in its paste command, and that repository was added to the case list. Nothing in this entry is attributed to a person or to a group.
* **Case `windows-defender-cc-lure-repos`, one more host added.** `fastpkg64.cc` was added as a delivery host later on the same day, because a lure README created on 2026-11-26 names it in its paste command. Nothing was retrieved from that host, so what its script does is not known.

## 2026-11-25

* **Case `windows-defender-cc-lure-repos`, page rewritten.** The case page was rewritten on 2026-11-25 to follow the victim's path first and to carry fewer figures. No finding, indicator or credit changed, and the star-rings section of the same day was shortened to one paragraph.
* **Case lists, repository status added.** Lure repository rows in `indicators.csv` can now end their `details` cell with `status` and `status_since`, described under "Repository status" in `METHOD.md`. The nine columns are unchanged, and no other cell of any row changed with this addition. From that day on, the automatic publish carries status changes at most once a day, and a large batch of new `not_found` or `replaced` waits for a manual check.

## 2026-11-24

* **Feed and case lists, layout change.** The three first-finder columns (`first_finder`, `vendor_seen_at` and `days_ahead`) are gone from every published file. Every day file published in the old layout was rewritten once to drop those columns, and the seven columns they kept are unchanged, with no row added or removed. Each case's `indicators.csv` now has five more columns (`role`, `description`, `linked_to`, `recorded`, `details`), and `METHOD.md` says what each one holds. The indicator table on each case page lost its first-finder column. The STIX and MISP files did not carry these fields and were not rewritten for this change, so no STIX id moved.
* **Feed, `first_seen` on 241 lure repositories.** For 241 repository rows first published on 2026-11-21, `first_seen` held the repository's last push time (2026-10-01 to 2026-11-20), not the time I first recorded it. Each now holds the time the repository was first recorded here (2026-11-21, shortly after 00:00 UTC; the read itself was made on 2026-11-20). Corrected in `feed/2026-11-21.csv` and `feed/rolling-30d.csv`. No indicator was added or removed, and no first-finder claim was affected (none was made for these rows).

## 2026-11-21

* **Feed, duplicates.** The day file for 2026-11-21 repeated all 125 indicators of 2026-11-20, and `rolling-30d.csv` listed those 125 twice, for about half an hour after 00:00 UTC. Both were replaced the same day. From this date a day file holds only what was first published that day, and the rolling file is the current list of what was first published in the last 30 days. `feed/README.md` and `METHOD.md` now say so.
* **Feed, STIX ids.** Indicator ids in the STIX files were different on every run. They are now stable (UUIDv5 of type, value and case). Ids in the 2026-11-20 file were not changed.
* **Case `windows-defender-cc-lure-repos`, scope narrowed and case extended.** The title and summary said the lure repos deliver the analysed stealer. That was shown only for the download chain that was run (`devtools8[.]lol` with `toolget2[.]lol`, and `quickrun31[.]cc`); for the other delivery hosts the payload was never retrieved. The text now says so. Added the same day: four delivery hosts, a second build's server, page and contract, three file hashes and 241 lure repositories found by a second crawl.

The first case was published on 2026-11-20.
