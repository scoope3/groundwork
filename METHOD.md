# Method

How a finding gets from a candidate to this repository, and what the published columns mean.

## From candidate to case

Candidates come from scheduled hunting over public sources. A candidate becomes a case only when two independent sources agree on it, or when one source is confirmed by a sandbox run. I then label every piece of evidence by hand. Nothing is attributed automatically.

A case is published when I have decided it. Cases that were opened and turned out to be noise are closed and never appear here, but they still count against the reliability score of the evidence types that suggested them.

## Evidence scope

| Scope | What it can establish |
| --- | --- |
| operator | the same person or group controls two things, from an identifier that is tied to a controller rather than to the software |
| kit | two things run the same software or kit, which does not by itself mean the same operator |
| context | the claim is more plausible, but on its own links nothing |

The specific signals behind each row are named on the case page only to the extent needed to judge it, not as a recipe.

An attribution to an operator is never made on kit or context evidence alone.

## False-positive rate

Each evidence type has a measured false-positive rate, the share of past proposals of that type that I rejected after looking. It is recomputed from my decisions and published with every row. Types with no history start at an assumed 50% and earn their number. The point is that a reader can weigh a row without trusting my judgement about it.

## First-finder record

For every published indicator I record whether it was already present in OSV, URLhaus, ThreatFox, VirusTotal or a vendor publication at the time I published it, and if so the earliest timestamp I could find. `first_finder` is true when none of them had it; `days_ahead` is the gap to the first vendor, negative when a vendor was first. The check is automated and conservative; a vendor source I did not check may have had it earlier.

## Verification

When a case involves a package or a web page, it was run in an isolated environment that records what the sample does. The result is hashed; the hash and date are published with the case, the record is kept privately and can be shared on request so a third party can verify it.

## Corrections

Mistakes are corrected in place and recorded in `CHANGELOG.md` with the date, what changed and why. Retracted indicators are removed from the rolling feed and marked in the day file they appeared in.

## Feed columns

| Column | Meaning |
| --- | --- |
| published_at | when the row was published, UTC |
| entity_type | domain, ip, package, publisher_account, url, email, asn |
| value | the indicator; hostnames are not defanged in the feed files |
| category | the research category the case belongs to |
| case | the case directory under `cases/` |
| evidence_types | the evidence types behind the row, semicolon separated |
| first_seen | when I first observed the entity |
| first_finder | true when no checked public source had it at publication |
| vendor_seen_at | the earliest vendor timestamp found, with the source |
| days_ahead | days between my publication and the first vendor, negative when a vendor was first |
