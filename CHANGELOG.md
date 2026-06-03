# OCPL Changelog

---

## v1.1 — 2026-06-03 (Current)

**Breaking from v1.0:** Projects using v1.0 should update to v1.1. The conditions are substantially the same; v1.1 fixes structural issues that made v1.0 problematic as a standalone legal instrument.

### Fixed
- Condition 5 (Constitutional Invariants): embedded the 10 principles directly; removed external reference to "RFC 0001" which could be modified independently of the license
- Condition 1 (Protocol Openness): replaced "canonical OpenKO protocol specifications published in the rfcs/ and specs/ directories of the canonical repository" with "authoritative specification repository designated by the licensor" — more precise and usable by non-OpenKO projects
- Condition 6 (Attribution): added "lineage record is permanent and survives stewardship transitions"
- Condition 7 (Patent Non-Aggression): added "survives any transfer of the patent"

### Added
- Preamble: states purpose and intent (commercial activity explicitly encouraged)
- Dependency Boundary section: explicit statement that OCPL does not propagate to linked dependencies
- License Compatibility section: names compatible inbound licenses (MIT, Apache 2.0, GPL v2+, LGPL, AGPL, MPL 2.0, ISC, BSD, CC0)
- Outbound Compatibility section: clarifies distribution as part of GPL v3 / AGPL v3 combined works
- Extensions section: documents OCPL-Format, OCPL-Tool, OCPL-Model extension system

---

## v1.0 — 2026-06-03 (Superseded)

Initial version. Shipped with the OpenKO protocol scaffold. Issues documented in [versions/v1.0.md](versions/v1.0.md).
