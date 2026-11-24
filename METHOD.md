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

## Indicator columns

Each case directory holds `indicators.csv`, the full current list of what is published for that case. The first four columns name the indicator and the evidence behind it. The next five describe the indicator, and every one of them comes only from accepted evidence of that case. A row with no accepted evidence of a type listed below has those five cells empty.

| Column | Meaning |
| --- | --- |
| type | The kind of indicator, one of domain, ip, package, publisher_account, url, email, asn, contract_address or crypto_address. |
| value | The indicator itself, written in full, with hostnames left undefanged in this file. |
| evidence_types | The evidence types behind the row now, separated by semicolons when there are several. |
| scopes | The scopes of that evidence (operator, kit or context), separated by semicolons when there are several. |
| role | A fixed name for what the indicator does in the case, taken from the table below for each evidence type. |
| description | A fixed sentence for each evidence type, taken from the table below and never from text an attacker wrote. |
| linked_to | The host name of another indicator in the same file that this one points at, filled only as described below. |
| recorded | The day the earliest observation behind the row was written into my store, as a UTC day. |
| details | A short list of `key=value` pairs separated by semicolons, with only the keys listed below. |

`recorded` is the day an observation was written into my store, and it is not a sighting. For indicators that came in with a batch research import it is the day of the import, so many rows share one day.

`linked_to` can be filled for a lure repository with the delivery host recorded for it in the evidence. It can also be filled for a dead-drop page with the command-and-control host its encrypted value decrypts to. The cell only ever holds a host name, and it is filled only when that host is itself a row of the same file with the matching evidence type. In every other case the cell is empty and the sentence says nothing about a link. A dead-drop value that decrypts to an IP address or to anything else that is not a host name gives no link. A row that carries two evidence types that could each hold a link has no link at all. When a linked host is taken back, the link and its sentence leave the rows that named it at the next publication.

| Evidence type | role | description | details keys |
| --- | --- | --- | --- |
| lure_repo | lure repository | "GitHub repository recorded as a lure for the delivery host in linked_to" when `linked_to` is filled, and "GitHub repository accepted as a lure of this case" when it is empty | owner_account_created |
| lure_delivery_domain | delivery host | "Domain that lure repository READMEs named as the place to download from" | registered, registrar |
| next_stage_host | next-stage host | "Host the first-stage script fetched its next stage from" | none |
| stealer_c2 | stealer command-and-control host | "Command-and-control host recovered by decrypting a value stored in the sample" | port, contacted_by_me |
| third_party_c2 | command-and-control host (third-party report) | "Reported in a third-party publication; not verified here" | reported |
| dead_drop | dead-drop page | "Public page holding an encrypted pointer to the command-and-control host in linked_to" when `linked_to` is filled, and "Public page holding an encrypted pointer to a command-and-control host" when it is empty | none |
| resolver_contract | dead-drop smart contract | "Smart contract holding an encrypted pointer to a command-and-control host" | chain, created, selector |
| deployer_wallet | contract deployer wallet | "Wallet recorded as the deployer of a dead-drop smart contract" | chain |

A row with two or more evidence types joins their roles with ` | ` and joins their sentences with ` | `, both in alphabetical order of the evidence type names. When two of those evidence types give the same key, the key is printed once, from the first type in that order whose value has the expected shape.

| Key | Meaning |
| --- | --- |
| owner_account_created | The day the GitHub account that owns the lure repository was created, as recorded with the evidence. |
| registered | The day the delivery host's domain was registered, as recorded with the evidence. |
| registrar | The short name of the domain's registrar, as recorded with the evidence. |
| port | The port number in the server address that was decrypted from the sample, from 1 to 65535. |
| contacted_by_me | This key reads `no`, and it appears only when the evidence says I never contacted the host. |
| reported | The day the third-party publication reported the host, as recorded with the evidence. |
| chain | The name of the blockchain that holds the contract or the wallet, in lower case. |
| created | The day the dead-drop contract was created on its chain, as recorded with the evidence. |
| selector | The four-byte function selector recorded for the dead-drop contract in the evidence, in lower-case hex. |

Where several evidence rows of one type give the same key, the value of the row written latest is used. The one exception is `contacted_by_me`, and it is printed only when every one of those rows says the host was never contacted. A key whose stored value does not have its expected shape is left out of the row. Days are printed as `YYYY-MM-DD` exactly as they were stored. A stored day without a time carries no time zone, and a stored time gives its day only when that time is written in UTC. Nothing in these columns says whether an indicator is still online, because I have no pass yet that checks every published row again. Paths, file names, account numbers and the way an indicator was found are never published in these columns.

## Verification

When a case involves a package or a web page, it was run in an isolated environment that records what the sample does. The result is hashed; the hash and date are published with the case, the record is kept privately and can be shared on request so a third party can verify it.

## Corrections

Mistakes are corrected in place and recorded in `CHANGELOG.md` with the date, what changed and why. A retracted indicator leaves `rolling-30d.csv` at the next publication, and the case's `indicators.csv` as long as the case still has other indicators. A case page whose every indicator is withdrawn is taken down by hand and the takedown is recorded in `CHANGELOG.md`. The day files (CSV, STIX, MISP) are a dated record of first publication. After their own day the day files are normally left alone. Some corrections and the layout change have rewritten earlier day files, and each of those rewrites is listed in `CHANGELOG.md`. Check an old day file, and anything read from the STIX or MISP files, against `rolling-30d.csv` or the case's `indicators.csv`.

## Feed columns

The day files and `rolling-30d.csv` both have the same seven columns, listed below.

| Column | Meaning |
| --- | --- |
| published_at | The time the indicator was first published for that case, in UTC. |
| entity_type | The kind of indicator, one of domain, ip, package, publisher_account, url, email, asn, contract_address, crypto_address or sha256 (a file hash). |
| value | The indicator itself, written in full, with hostnames left undefanged in the feed files. |
| category | The research category that the case belongs to, as named on the case page. |
| case | The name of the case directory under `cases/` that holds the write-up. |
| evidence_types | The evidence types behind the row, separated by semicolons when there are several. |
| first_seen | The earliest time my store holds for the entity, in UTC. For a lure repository that is the time I first recorded it. For some other sources it is the first-seen time the source itself reported. |

Until the layout change recorded in `CHANGELOG.md` the feed files had three more columns about first finding. Every day file published in the old layout was rewritten once to drop those three columns, and the case files now carry the descriptive columns described above.
