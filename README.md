# cloud-itonami-lei-9845007375ebb04c6f49

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Nigerian National Petroleum Company Limited.**

This repository archives the publicly published Terms of Use of **Nigerian National
Petroleum Company Limited (NNPC Limited)**, with source-url and retrieval-date
provenance, per ADR-2607110300 (`cloud-itonami-lei-corporate-tos-catalog`,
`com-junkawasaki/root`). Read-only reference/archive repository — not a governed
Advisor/Governor actor.

Part of the **worldwide-scope extension** of the cloud-itonami-lei catalog (batch
AFRICA-UTIL-1, 2026-07-24/25).

## Company identity

- **Legal name**: Nigerian National Petroleum Company Limited (NNPC Limited)
- **LEI (ISO 17442)**: [9845007375EBB04C6F49](https://search.gleif.org/#/record/9845007375EBB04C6F49) (GLEIF entity-verified, NG)
- **Jurisdiction**: NG (Nigeria)
- **Website**: https://www.nnpcgroup.com
- **ISIC Rev.5**: 0610 (extraction of crude petroleum)
- **Public contact email**: contactus@nnpcgroup.com (published on the site's Contact Us page)

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of the archived Terms of Use.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record, including the public
  contact email sourced from the company's own Contact Us page.
- `facts.edn` — 9 verified registry facts with per-fact provenance. **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The identity table above used to be assertions with nothing in the repository
behind them. `facts.edn` now carries them as data, and every value in it was read
out of a public registry response whose URL and retrieval time sit next to the
value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO URLs were fetched and nine facts recorded — the LEI record
(legal name as GLEIF spells it, **`NIGERIAN NATIONAL PETROLEUM COMPANY
LIMITED`**, upper case, `en`; entity **ACTIVE**, registration **ISSUED**,
**`PARTIALLY_CORROBORATED`** / `CONFORMING` — entity status and registration
status are different fields and are recorded separately, and the corroboration
level is the middle grade, not the `FULLY_CORROBORATED` most listed-company
records in this family carry; legal address and headquarters the same,
`NNPC TOWERS CENTRAL BUSINESS DISTRICT, Herbert Macaulay Way, 900001, ABUJA,
NG-FC, NG`, as GLEIF spells it; entity creation date `2021-09-21` — the CAMA-era
incorporation, not the 1977 statutory corporation the company's history pages
describe, which held no LEI and is not in GLEIF's data; initial LEI registration
`2023-11-22`, last updated `2026-03-03`, next renewal `2026-11-22`; one BIC,
**`NNPCNGLAXXX`**; S&P Global id `9012522`; no OpenCorporates id), its ISIN
mapping (**0** instrument identifiers — a measured zero read from
`meta.pagination.total` of the cited page: GLEIF maps no ISINs to this LEI,
which says nothing about bonds issued through separate financing vehicles
holding their own LEIs — none was looked for here), its managing LOU and
LEI-issuer accreditation (**Ubisecure Oy** / RapidLEI, FI, accredited
2018-04-03 — a commercial Finnish LOU, not a Nigerian authority), registration
authority `RA000469` (**Corporate Affairs Commission** — `www.cac.gov.ng`,
serving Nigeria only — where the entity is company number `1843987`), ISO 20275
legal form `FHZY` (**`Private company limited by shares`**, NG), and **both
consolidation levels**: no parent at either level, each level carried as a
reporting-exception entity with category
`DIRECT_ACCOUNTING_CONSOLIDATION_PARENT` /
`ULTIMATE_ACCOUNTING_CONSOLIDATION_PARENT` and reason **`NATURAL_PERSONS`**.
Nine of the eleven URLs answered `200` when the file was written; the
`direct-parent` and `ultimate-parent` endpoints answered `404` because GLEIF
publishes the *exception* side of that pair for this entity, which the checker
treats as a fact rather than a failure.

That exception reason is the finding of this record. `NATURAL_PERSONS` is
GLEIF's code for "controlled by natural person(s) with no consolidating legal
entity above" — yet this is the company that Nigeria's Petroleum Industry Act
2021 places in state hands, and the company's own site describes it as wholly
owned by the Federation. Whether shares held through government nominees are
better described by GLEIF's `NATURAL_PERSONS` or by a government-entity parent
is a question about the filing, not answered by it; the filing is what it is,
and it is recorded here unedited. The legal form is the second half of the same
finding: `FHZY` — a *private* company limited by shares under CAMA 2020, the
same form as any Lagos trading company, carrying a US$-billions national oil
company. Neither the Federation nor any ministry appears anywhere in the
record: GLEIF's relationship data for this LEI consists of the two exceptions
and nothing else.

GLEIF records **0 direct children** for this LEI (`meta.pagination.total` of
the cited `direct-children` page). That is a measured zero about what GLEIF's
relationship data holds, not a claim that the company has no subsidiaries — the
NNPC group's own site names dozens (NNPC Trading, NNPC Retail, the refining
companies); a company appears as a GLEIF child only if it holds an LEI and
reports the relationship, and none does. For a group this size, the empty
relationship graph — no parent, no children, no ISINs — is itself the shape of
the record: the LEI exists for counterparty identification (the BIC
`NNPCNGLAXXX` sits on the record for the same reason), not because any
securities regulator compelled a group structure filing.

The check has three exit codes, not two: `0` when every cited URL answered and
every recorded value still matches, `1` when a citation broke or a value
drifted (each difference is named, with the recorded and live values side by
side), and `3` when the check could not be performed at all — `facts.edn`
missing or empty, or GLEIF unreachable at the transport level — because a check
that could not run must not look like a check that ran and found nothing.
Before this landed, all three were shown against the live API: unmodified →
`0`; `:company/jurisdiction` edited from `NG` to `FR` → `1`, naming
`gleif-lei-record :company/jurisdiction` as `DRIFT`; the
`gleif-direct-children-count` entity deleted → `1`, naming it as `ADDED`;
`facts.edn` absent → `3` (`INCONCLUSIVE … Refusing to report a pass`). Each
break was diffed against a backup before its run was trusted, and the file was
restored byte-identical afterwards.

## Design rationale

See ADR-2607110300 and the worldwide-scope extension ledger
(`2607110300-cloud-itonami-lei-corporate-tos-catalog.worldwide-progress.edn`) in
`com-junkawasaki/root` (`90-docs/adr/`).
