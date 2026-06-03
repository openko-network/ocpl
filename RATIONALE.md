# OCPL Rationale — Why Each Condition Exists

This document explains the design thinking behind each OCPL condition: what failure mode it prevents, what was rejected and why, and how it was shaped.

---

## Why Not MIT or Apache 2.0?

MIT and Apache 2.0 are excellent licenses for libraries and general-purpose software. They are intentionally minimal — permissive by design. For coordination protocol software, that minimalism is a vulnerability.

Three failure modes that permissive licenses do not prevent:

**Protocol capture:** A well-funded actor forks the software, extends the protocol with proprietary features that only their nodes implement, and uses patent threats or trade secrets to prevent others from implementing the extensions. Over time, their proprietary fork becomes the de-facto network. The "open" protocol becomes legacy.

**User lock-in:** An operator runs the software as a service but modifies it to prevent users from exporting their identity, data, or reputation. Users cannot leave without losing everything they've built. What was a voluntary cooperative becomes a captured platform.

**Governance capture:** A corporation acquires the primary development entity and uses that control to alter the protocol to serve extraction rather than public good. The federated governance that made the network worth joining is dismantled from within.

MIT and Apache prevent none of these. OCPL was written to prevent all three.

---

## Condition 1: Protocol Openness

**What it prevents:** Protocol capture via proprietary extensions + patent threats.

**The failure mode without it:** Actor A forks the network, adds proprietary gossip extensions, patents the new wire format, and sues anyone implementing compatible nodes. Over 3-5 years, their nodes become the default because they have features nobody else can implement. The "open" network is now captured.

**Why "interoperable with canonical specifications":** It's not enough to publish specs — you must stay interoperable with them. A fork that adds proprietary-only extensions and deprecates the open baseline is still a form of capture.

**Rejected alternatives:**
- "Must publish all extensions": too broad — limits legitimate private experimentation
- "Must contribute extensions back": too restrictive — kills commercial incentive for improvement
- "Must accept connections from any conforming node": this is what "interoperable" means operationally

---

## Condition 2: Identity Sovereignty

**What it prevents:** Identity hostage-taking.

**The failure mode without it:** Users build reputation, agent configurations, delegation chains, and mission history over years. An operator locks the export endpoint. Users cannot leave without starting over. The voluntary network becomes a platform with switching costs equal to losing your entire professional identity.

**Why all four sub-points:**
- (a) Key material export: you must be able to prove you are you, elsewhere
- (b) History export: reputation built through contribution is yours, not the operator's
- (c) Migration: the right to leave must be exercisable, not theoretical
- (d) Delegation revocation: you must be able to de-authorize agents immediately

**Rejected alternatives:**
- "Must provide an export button": too easy to implement a broken one
- "Must support portable DIDs": necessary but not sufficient — data without keys is useless

---

## Condition 3: Data Portability

**What it prevents:** Practical lock-in even when legal rights exist.

**The failure mode without it:** Condition 2 gives users the right to export. Condition 3 makes that right exercisable. Without a 30-day SLA and "at no charge," an operator can honor the letter of Condition 2 while making the export practically impossible (6-month wait, $500 fee, proprietary format).

**Why 30 days:** Long enough to be operationally reasonable. Short enough that it's not a meaningful barrier.

**Why "machine-readable open format":** An export that requires the operator's software to read is not portable. The format must be documented and independently parseable.

---

## Condition 4: No Lock-in

**What it prevents:** Patent-based and contractual capture.

**The failure mode without it:** An actor implements the protocol, then patents specific parts of the wire format or cryptographic construction. They selectively enforce those patents against competitors. The protocol remains "open" in the sense that the spec is published, but it cannot be implemented freely.

**Why four sub-points:**
- (a) Protocol implementations: you can implement the spec
- (b) Data formats: you can read and write the formats
- (c) Federation: you can connect to the network
- (d) Forking: you can operate independently

**Relationship to Condition 1:** Condition 1 is about protocol openness at the specification level. Condition 4 is about enforcement — the legal mechanisms that could be used to prevent implementation even of openly published specs.

---

## Condition 5: Constitutional Invariants

**What it prevents:** Governance capture from within.

**The failure mode without it:** A well-intentioned project becomes successful. A corporation acquires the primary development entity. The new owners, under commercial pressure, begin modifying governance to centralize control, extract revenue, or silence public-good missions. They have the legal right to do so under MIT/Apache. The network that attracted contributors because of its principles is dismantled by those who inherited it.

**Why embed in the license (not reference an external document):** The original OCPL v1.0 referenced "RFC 0001" in an external repository. That document could be changed. A license that references a mutable external standard is not a stable legal instrument. The 10 principles are embedded directly in OCPL v1.1 so they cannot be amended by changing a RFC.

**Why 10 principles and not fewer:** Each addresses a specific capture vector. "No permanent central authority" + "governance remains federated" cover the organizational capture vector. "Protocols remain open" + "knowledge remains portable" cover the technical capture vector. "Identities remain sovereign" covers the individual capture vector. Fewer principles would leave gaps.

**Rejected alternatives:**
- "Must use federated governance": too vague to enforce
- "Board must have community representatives": too easy to make nominal
- Reference GPL's copyleft mechanism: copyleft prevents code closure but not governance capture

---

## Condition 6: Attribution

**What it prevents:** Credit erasure and false origin claims.

**Practical purpose:** Attribution in open-source projects does real work — it drives reputation, signals the origin of design decisions, and creates accountability. A fork that silently removes attribution can be mistaken for the canonical version, creating confusion about which entity to trust for security updates.

**Why "lineage record is permanent":** Consistent with the stewardship model — even when a project changes hands, the original creators retain credit.

---

## Condition 7: Patent Non-Aggression

**What it prevents:** Submarine patent attacks on protocol implementations.

**The failure mode without it:** A contributor patents a cryptographic construction they contribute to the protocol. Years later, they (or a successor who acquires the patents) sues competing implementations. This is the open-source patent threat that has damaged multiple communities.

**Why "perpetual and irrevocable":** A revocable patent grant is worthless as a long-term protection. Contributors who hold relevant patents make a permanent, irrevocable commitment on contribution.

**Relationship to Apache 2.0:** Apache 2.0's patent grant covers code contributions; it terminates if you sue over Apache-related patents. OCPL's grant covers *protocol implementations specifically* and is non-revocable. The two are compatible and OCPL's is slightly stronger for the protocol case.

---

## Condition 8: Source Availability for Network Services

**What it prevents:** Proprietary forks that run as hosted services without giving back.

**The failure mode without it:** An actor takes the OCPL software, makes significant improvements, runs it as a hosted service for millions of users, and never releases the improvements. The improvements are effectively proprietary. The open-source project falls behind its own fork. (The "Amazon problem" that motivated AGPL.)

**Why "modifications only" and not the entire service:** OCPL does not require releasing proprietary application code layered on top of OCPL infrastructure. Only modifications to OCPL-licensed code itself must be released. Building a closed-source application that uses OCPL infrastructure is explicitly permitted.

**Why "publicly accessible" service, not internal use:** Internal tools used only within an organization are not required to release. Only software made available to the public triggers this condition. This is the same scope as AGPL.

---

## Dependency Boundary: Why Explicit

Without an explicit dependency boundary, every team using an OCPL library faces the question: does OCPL propagate to our code? The answer is no — OCPL is not copyleft in the GPL sense — but stating it explicitly prevents legal uncertainty and adoption friction.

The dependency boundary was modeled on Apache 2.0's handling of this (Apache projects can use GPL code without Apache propagating to GPL portions) and the Linux kernel's syscall exception (GPL does not propagate through syscall interfaces).

---

## Compatibility Section: Why Explicit

OCPL was designed to coexist with the Rust ecosystem (MIT/Apache 2.0 dominated), the Python ecosystem (PSF/MIT dominated), and the Linux kernel ecosystem (GPL v2/v3). Without an explicit compatibility statement, legal teams in organizations considering OCPL projects face unnecessary research. The compatibility section eliminates that friction.

---

## Extension System: Why Modular

Different project types have different additional needs:

- A **format specification project** needs to guarantee that the format remains readable without the reference implementation — the core OCPL doesn't say this explicitly.
- An **AI model project** needs to address training data lineage and weight availability — not relevant to coordination protocol software.
- A **developer tool** needs to guarantee a free local tier — not relevant to protocol implementations.

Rather than one monolithic license that tries to cover everything (and becomes unwieldy), OCPL has a core + named extensions. Each extension adds conditions for a specific domain; none may remove core conditions.

---

## What Was Deliberately NOT Included

**Copyleft propagation to linked code:** OCPL is not GPL. It does not require downstream users of OCPL libraries to release their own code under OCPL. The dependency boundary clause makes this explicit. Copyleft propagation would make OCPL unusable in commercial application layers built on top of the protocol — which is explicitly permitted.

**Revenue sharing requirements:** Some licenses (Commons Clause, BUSL) restrict commercial use or require revenue sharing. OCPL does not. Commercial activity is encouraged. The network benefits from commercial participants; restricting them would reduce ecosystem health.

**Field-of-use restrictions:** No "non-military use" clauses, no "non-surveillance" clauses. These restrictions are unenforceable in many jurisdictions and create adoption barriers for legitimate uses. The Constitutional Invariants (Condition 5) are a better mechanism — they prohibit specific behaviors (centralization, surveillance, lock-in) rather than restricting who can use the software.

**Mandatory contribution-back:** Some licenses require that modifications be contributed back to the project. This is too restrictive for commercial participants who legitimately want proprietary improvements at the application layer. Only hosted modifications of the OCPL core (Condition 8) must be published.
