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

Each case directory holds `indicators.csv`, the full current list of what is published for that case. The first four columns name the indicator and the evidence behind it. The next six describe the indicator, and they come only from accepted evidence of that case, except the repository status that `details` can end with. A row with no accepted evidence of a type listed below has those six cells empty. The last column, `source_detail`, comes from a read of the repository's README by a tool of mine and is described under "Source".

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
| source | One or more fixed words for the kind of material the indicator was read from, as listed under "Source" below, or empty. |
| source_detail | A short list of `key=value` pairs about a read of the repository's README, with only the keys listed under "Source" below. |

`recorded` is the day an observation was written into my store, and it is not a sighting. For indicators that came in with a batch research import it is the day of the import, so many rows share one day.

`linked_to` can be filled for a lure repository with the delivery host recorded for it in the evidence. It can also be filled for a dead-drop page with the command-and-control host its encrypted value decrypts to. The cell only ever holds a host name, and it is filled only when that host is itself a row of the same file with the matching evidence type. In every other case the cell is empty and the sentence says nothing about a link. A dead-drop value that decrypts to an IP address or to anything else that is not a host name gives no link. A row that carries two evidence types that could each hold a link has no link at all. When a linked host is taken back, the link and its sentence leave the rows that named it at the next publication.

| Evidence type | role | description | details keys |
| --- | --- | --- | --- |
| lure_repo | lure repository | "GitHub repository recorded as a lure for the delivery host in linked_to" when `linked_to` is filled, and "GitHub repository accepted as a lure of this case" when it is empty | owner_account_created, status, status_since |
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

### Repository status

A lure repository row can end its `details` with two more keys, `status` and `status_since`. Roughly once a day, and never twice within twenty hours, I ask GitHub's API whether each published lure repository with a standard GitHub address still answers there. I ask for the repository's numeric id, its current owner and name, and its creation date. Each query also reads one fixed repository of GitHub's own, as a check that the answer can be trusted. Before I call a repository not found, I ask a second API endpoint and use only whether it returns 404.

| status | Meaning |
| --- | --- |
| up | The address answered with the repository id I have on record, under the same owner and name, ignoring letter case. |
| moved | The repository id I have on record answered under another owner or name, and the new name is not published. |
| replaced | The address answered with a different repository id from the one on record, or with a repository created after the row was recorded. |
| not_found | GitHub answered "not found" on two reads at least twelve hours apart, and a second API endpoint agreed on the later read. |
| unverified | The address answers with a repository created on or before the row was recorded, but I have no id on record to confirm it is the same one. |

`status_since` is the UTC day of the read that first showed the current status after it last changed. It is the day I saw the change, and the change itself can be older. For `not_found` it is the day of the second read, the one that confirmed it. A row with no `status` has not been given one yet, for example because it was never read, was not found only once, or has an address I cannot ask about.

The id on record is the repository id saved in the row's accepted evidence, when that evidence has one. For a row recorded without an id, the first repository that answers before any status is stored becomes the id on record, but only when GitHub reports it was created on or before the day the address was first recorded as a lure. A younger repository at that address is reported as `replaced`. A row that was not found on its last read, or that was `not_found` or `replaced` before it had an id, gets no id from my reads, so a repository created on or before that day answering there later makes it `unverified`. A repository put at the address before my first read cannot be told apart from the original by these reads.

A status describes the address and says nothing about what the repository holds today. `up` does not mean the lure text is still in the README, and `not_found` does not say whether the owner, GitHub or anyone else removed it. A repository can be made private and public again, so a status is not a reason to stop blocking an indicator. The status keys appear only in `indicators.csv`, and the feed files, the STIX files and the MISP files do not carry them.

### Source

`source` says what kind of material an indicator was read from, and it does not say how I came to look at that material. The cell holds one of the fixed words below, or several joined by ` | ` when the evidence supports more than one. The cell is empty when the accepted evidence of a row does not record what it was read from, so an empty cell is no statement about the row.

| Word | Meaning |
| --- | --- |
| readme command | The indicator is a repository recorded with the delivery host its README named, or a host that lure repository READMEs named as the download place. |
| script read | A script that I retrieved and read named paths on this host. |
| sandbox run | The next-stage host was seen on the wire during a run in a sandbox. |
| static analysis | The value was taken from the analysis of a sample, such as an address recovered by decryption or a page or contract that the sample reads. |
| chain record | The value comes from public blockchain records, such as the deployer of a contract. |
| third-party report | The value was reported in another researcher's publication and was not verified here. |

For a lure repository, `source_detail` can hold `readme_sha256` and `readme_read`. The first is the SHA-256 of the README found at the repository's address when a tool of mine read it, and the second is the UTC day of that read. The pair is printed only when that read found the row's current `linked_to` host in the README. It describes the README on the day of the read, and that day can be later than the day the repository was first recorded. A row has no pair when it has no `linked_to` host, when no such read has been made, when the read did not find the host in the README or found no README, or when the README could not be hashed whole.

## Verification

When a case involves a package or a web page, it was run in an isolated environment that records what the sample does. The result is hashed; the hash and date are published with the case, the record is kept privately and can be shared on request so a third party can verify it.

## Corrections

Mistakes are corrected in place and recorded in `CHANGELOG.md` with the date, what changed and why. A retracted indicator leaves `rolling-30d.csv` at the next publication, and the case's `indicators.csv` as long as the case still has other indicators. A case page whose every indicator is withdrawn is taken down by hand and the takedown is recorded in `CHANGELOG.md`. The day files (CSV, STIX, MISP) are a dated record of first publication. After their own day the day files are normally left alone. Some corrections and the layout change have rewritten earlier day files, and each of those rewrites is listed in `CHANGELOG.md`. Check an old day file, and anything read from the STIX or MISP files, against `rolling-30d.csv` or the case's `indicators.csv`.

## Feed columns

The day CSV files and `rolling-30d.csv` share the seven columns below, and each kind of file then adds columns of its own.

| Column | Meaning |
| --- | --- |
| published_at | The time the indicator was first published for that case, in UTC. |
| entity_type | The kind of indicator, one of domain, ip, package, publisher_account, url, email, asn, contract_address, crypto_address or sha256 (a file hash). |
| value | The indicator itself, written in full, with hostnames left undefanged in the feed files. |
| category | The research category that the case belongs to, as named on the case page. |
| case | The name of the case directory under `cases/` that holds the write-up. |
| evidence_types | The evidence types behind the row, separated by semicolons when there are several. |
| first_seen | The earliest time my store holds for the entity, in UTC. For a lure repository that is the time I first recorded it. For some other sources it is the first-seen time the source itself reported. |

A day CSV file adds `role`, `linked_to` and `source`, with the meanings given under "Indicator columns". A row first published on or after 2026-11-26 keeps the three cells of the last publication made on its own day, and later publications leave them as they are. `rolling-30d.csv` adds `role`, `description`, `linked_to`, `source` and `details`, and it is rebuilt at every publication, so its cells show each row as it is now. The feed files never carry `status` or `status_since`, and the current status of a repository is in the case's `indicators.csv`. File-hash rows in the feed files have the added cells empty, and the case's `files.csv` describes each file. The STIX and MISP day files are unchanged by these columns.

Until the layout change of 2026-11-24 the feed files had three more columns about first finding, and every day file in that layout was rewritten once to drop them. On 2026-11-26 every day CSV file published before that day was rewritten once to add `role`, `linked_to` and `source`. Those cells hold the values each row had when the rewrite was made on 2026-11-26, and they are empty for file-hash rows and for rows that were no longer published then. No row was added to or removed from a day file by either rewrite.

## File hashes

A case directory can hold `files.csv`, with one row for each file whose hash is published for the case.

| Column | Meaning |
| --- | --- |
| sha256 | The SHA-256 of the file as I recorded it for the case. |
| kind | A fixed word for what the file is, one of loader script, archive, stealer build or macOS binary, or empty when no fixed word is recorded. |
| delivered_by | The host recorded as serving the file, filled only when that host is a delivery host or next-stage host row of the same case. |
| source | How the file was obtained, either sandbox run or retrieved script, or empty when no fixed word is recorded. |

File names are not published, because a file name is text chosen by whoever served the file.
