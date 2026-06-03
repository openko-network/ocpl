# OCPL Compatibility Matrix

How OCPL interacts with other licenses — as inbound dependencies, outbound distributions, and in combined works.

---

## The Core Rule

**Dependency Boundary:** OCPL conditions apply to the covered work (the OCPL-licensed code). They do not propagate to libraries the covered work links against. Those libraries keep their own licenses.

This means: using MIT/Apache/GPL libraries in an OCPL project is always fine. The libraries stay under their license. Your code stays under OCPL.

---

## Inbound Compatibility (libraries you USE in an OCPL project)

### MIT License ✅ Compatible

**Example libraries:** tokio, serde, serde_json, anyhow, thiserror, pydantic, httpx, react, typescript

**How it works:** MIT grants blanket permission to use, modify, and distribute. You may incorporate MIT code into an OCPL project, distribute it alongside your OCPL code, and the MIT portions remain under MIT. No conflict whatsoever.

**In practice:**
```
Your OCPL project links tokio (MIT)
→ tokio stays MIT
→ Your project code is OCPL
→ Distribute: tokio under MIT, your code under OCPL
→ ✅ No conflict
```

---

### Apache 2.0 ✅ Compatible

**Example libraries:** libp2p, ed25519-dalek, opentelemetry, most Google/Meta/AWS open-source

**How it works:** Apache 2.0 grants blanket permission plus a patent license. Apache's patent termination clause (if you sue over patents, your license terminates) is compatible with OCPL Condition 7 (Patent Non-Aggression) — they reinforce each other.

**Note:** Apache 2.0 requires preservation of NOTICE files. Keep those files in your distribution alongside your OCPL license notice. Both requirements are compatible.

```
Your OCPL project links ed25519-dalek (Apache 2.0)
→ ed25519-dalek stays Apache 2.0
→ Distribute: ed25519-dalek under Apache 2.0 + NOTICE, your code under OCPL
→ ✅ No conflict
```

---

### GPL v2 ⚠️ Use caution

**Example libraries:** Some older Linux utilities, some older embedded software

**The issue:** GPL v2 §6 says "you may not impose any further restrictions on the recipients' exercise of the rights granted herein." OCPL Condition 5 (Constitutional Invariants) restricts what *distributors* may do, which GPL v2 could interpret as a "further restriction."

**Practical guidance:**
- Avoid GPL v2-only libraries in core protocol implementations
- Most GPL v2 libraries are actually "v2 or later" — if so, use them as GPL v3 (see below)
- If you must use a GPL v2-only library, consult the specific terms; many have exceptions for standard system libraries

---

### GPL v3 ✅ Compatible (with care)

**Example libraries:** Many GNU utilities, some scientific software

**How it works:** GPL v3 §7 explicitly allows "additional terms" that are user-protective. OCPL's conditions (protocol openness, identity sovereignty, no lock-in) protect users, not restrict them. OCPL Condition 8 (Source Availability for Network Services) aligns directly with AGPL §13.

**The combined work rule:** If you link GPL v3 code into your OCPL project and distribute the combined work, the combined work must be distributable under GPL v3. OCPL is compatible as an outbound license for GPL v3 combined works — the OCPL conditions for your portions are preserved, the GPL v3 conditions govern the GPL portions, and both sets of conditions apply to the combined work.

```
Your OCPL daemon links a GPL v3 library
→ Combined binary: must be distributable under GPL v3
→ OCPL conditions preserved for your portions
→ GPL v3 conditions apply to GPL portions
→ ✅ Compatible (both sets of conditions apply)
```

---

### LGPL v2.1 / v3 ✅ Compatible

**Example libraries:** glibc, Qt (LGPL), some scientific libraries

**How it works:** LGPL allows linking without the library's copyleft propagating to your code, provided you allow users to swap the LGPL library. An OCPL project using an LGPL library via dynamic linking is clean: the LGPL library stays LGPL, your code stays OCPL. LGPL's "allow relinking" requirement is compatible with OCPL's no-lock-in condition.

---

### AGPL v3 ✅ Compatible

**Example libraries:** Some databases (older MongoDB, CockroachDB open editions), some network services

**How it works:** AGPL v3 adds the "network use" trigger to GPL v3 — if you offer the software over a network, you must provide source to users. OCPL Condition 8 is functionally equivalent for OCPL-licensed modifications. The two requirements are compatible and mutually reinforcing. GPL v3 and AGPL v3 are explicitly compatible with each other, and OCPL's compatibility with GPL v3 extends to AGPL v3.

---

### MPL 2.0 ✅ Compatible

**Example libraries:** Some Mozilla projects, some Rust crates (e.g., older versions of some crates)

**How it works:** MPL 2.0 is file-level copyleft — modifications to MPL files must stay MPL, but MPL files can be combined with differently-licensed files in the same project. An OCPL project with MPL components: the MPL files stay MPL, the OCPL files are OCPL, both exist in the same codebase without conflict.

---

### ISC / BSD 2-Clause / BSD 3-Clause ✅ Compatible

Functionally equivalent to MIT for compatibility purposes. No conflict.

---

### CC0 1.0 ✅ Compatible (for documentation/data)

Public domain dedication. Zero restrictions. Use freely.

---

### Creative Commons (BY, BY-SA, BY-NC, etc.) ⚠️ Context-dependent

- CC-BY: Compatible for documentation
- CC-BY-SA: Compatible for documentation (ShareAlike is similar to copyleft)
- CC-BY-NC: **Not compatible** for any commercial use — OCPL explicitly permits commercial use
- CC-BY-ND: **Not compatible** — prohibits derivatives

---

### BSL / BUSL (Business Source License) ❌ Not compatible

BSL has a "change date" after which it converts to open source, but during the BSL period it restricts commercial use and production use. OCPL's permission for commercial use conflicts with BSL restrictions. Do not use BSL libraries in OCPL projects during the BSL period.

---

### Proprietary / Commercial Licenses ❌ Not compatible (as inbound)

If a library requires a proprietary license to use, its restrictions conflict with OCPL's Condition 4 (No Lock-in) and the spirit of the Dependency Boundary. Do not use proprietary libraries in the protocol core of an OCPL project. Proprietary integrations at the application layer (separate from the protocol implementation) may be acceptable depending on the specific terms.

---

## Outbound Distribution (distributing an OCPL project)

| Scenario | Result |
|---|---|
| Distribute as OCPL | ✅ Always fine |
| Distribute as GPL v3 + OCPL conditions preserved | ✅ Fine for combined works containing GPL v3 components |
| Distribute as AGPL v3 + OCPL conditions preserved | ✅ Fine |
| Distribute as MIT | ❌ Cannot: MIT drops the protection conditions |
| Distribute as Apache 2.0 | ❌ Cannot: Apache drops the protection conditions |
| Distribute as proprietary | ❌ Cannot: violates Condition 4 (No Lock-in) and Condition 8 |

---

## Worked Examples

### Example 1: Rust daemon using common crates

```toml
[dependencies]
tokio        = "1"          # MIT
serde        = "1"          # MIT/Apache 2.0
libp2p       = "0.54"       # MIT
ed25519-dalek = "2"         # Apache 2.0
anyhow       = "1"          # MIT/Apache 2.0
```

Your daemon code: OCPL-1.1

**Distribution:** ship each crate under its original license, ship your daemon code under OCPL. Include all license notices. ✅ Clean.

---

### Example 2: Python tool with stdlib + pydantic

```python
# stdlib: PSF License (permissive, always compatible)
# pydantic: MIT
# httpx: BSD 3-Clause
```

Your tool: OCPL + OCPL-Tool extension

**Distribution:** include OCPL license, include pydantic/httpx notices under their own licenses. ✅ Clean.

---

### Example 3: Project that needs a GPL v3 library

Your OCPL project wants to use `libgpg-error` (GPL v2+) for cryptography.

1. Check: is it "v2 or later"? If yes, treat as GPL v3.
2. Your combined binary must be distributable under GPL v3.
3. Your OCPL-licensed code portions must preserve OCPL conditions in source form.
4. Users receive: your source under OCPL (which is distributable under GPL v3), the GPL library source under GPL v3.
5. Both sets of conditions are satisfiable simultaneously. ✅

---

### Example 4: Someone forks your OCPL project and adds proprietary code

They can add proprietary features at the application layer (a closed-source client that calls your open protocol APIs). They **cannot**:
- Close the protocol specification (Condition 1)
- Remove user identity export (Condition 2)
- Remove data portability (Condition 3)
- Patent the protocol and block others (Conditions 4, 7)
- Remove the 10 constitutional invariants (Condition 5)

They must also provide source for their modifications if they run a public hosted service (Condition 8). ✅ The open core is protected; application-layer innovation is free.

---

## The Dual-License Option

Some projects use dual licensing to serve both communities:

```
Licensed under OCPL-1.1 OR Apache 2.0, at your option.
```

Under this model:
- Downstream users who need Apache 2.0 compatibility take Apache 2.0
- Downstream users who want OCPL's protections take OCPL
- The protocol openness protections only apply to OCPL users — Apache users can theoretically close forks

This is legitimate but weakens the network-level guarantee. Recommended only when broad ecosystem adoption trumps protocol protection.

---

## Questions Not Answered Here

This document covers the most common cases. For unusual combinations (obscure licenses, multi-jurisdiction distribution, patent-heavy domains), consult qualified legal counsel. OCPL is designed to be legally clear, but no license document is a substitute for legal advice in complex situations.
