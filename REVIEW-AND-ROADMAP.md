# OCPL Review and Roadmap

**Source:** scratch/ocpl/ocpl-review.md + scratch/ocpl/ocpl-feature-suggestions.md
**Status:** Design reference

---

## What OCPL Gets Right

### Framing around protocols, not morality

Most novel licenses fail because they become ideological or vague ("don't do evil," "for humanity"). OCPL focuses on concrete infrastructure properties: protocol openness, identity portability, anti-lock-in, federation integrity, governance continuity. Those are enforceable architectural principles. That framing gives OCPL a realistic chance of being taken seriously by legal teams and adopters.

### Clear positioning

The line "The conditions protect the network's integrity, not restrict legitimate business" immediately separates OCPL from anti-commercial licenses, faux-open licenses, and source-available traps. The effective message — "Build businesses freely. Just don't close the commons." — is a powerful and correct framing.

### Identity Sovereignty as the real differentiator

AGPL protects source. GPL protects code freedom. Neither protects portable identity, exportable social graph, federation continuity, interoperable governance, or protocol survivability. Modern lock-in is mostly identity lock-in, graph lock-in, and coordination lock-in. OCPL directly targets that. This is what makes the license feel modern rather than "yet another OSS license."

### The Dependency Boundary clause

Without an explicit boundary, potential adopters immediately ask: "Does OCPL infect my application code? Can I link Tokio? Can I use GPL dependencies?" The explicit dependency boundary eliminates a massive adoption barrier. Modeled correctly on Apache 2.0's handling and the Linux kernel syscall exception.

### Constitutional Invariants framing

Embedding the 10 principles directly in the license text (v1.1) rather than referencing an external RFC was the correct call. A license that references a mutable external standard is not a stable legal instrument. The invariants now cannot be amended by changing a separate document.

### OCPL's position in license space

| Type | Similarity |
|------|------------|
| AGPL | hosted-source reciprocity |
| Apache | patent awareness |
| MPL | scoped obligations |
| SSPL | network concerns |
| CC ShareAlike | commons preservation |

The closest conceptual relative is a "constitutional protocol commons license" — new territory that the existing OSS license landscape does not cover.

### CC0 license text

Publishing the OCPL license text itself under CC0 1.0 lowers adoption friction, encourages ecosystem use, allows derivative variants, and prevents license ownership politics. Good call.

---

## Gaps and Hardening Work

### 1. Enforce the three pillars everywhere

The thesis of OCPL sits in this table:

| Concern | MIT/Apache | OCPL |
|---------|------------|------|
| Protocol openness | ✗ | ✓ |
| Identity portability | ✗ | ✓ |
| Federation capture resistance | ✗ | ✓ |

Every clause in the license, every future RFC, every extension module should be traceable back to at least one of these three. Clauses that don't reinforce a pillar are candidates for removal.

### 2. Define the Core Constitutional Invariants explicitly

The current invariants are implied. They should be elevated into a formal normative section that courts and developers can reference directly:

1. **Protocol Openness** — Core network protocols MUST remain publicly documented and implementable without proprietary permission, undisclosed APIs, or trade-secret dependencies.
2. **Identity Sovereignty** — Users MUST be able to export their identities, credentials, keys, relationships, and protocol-relevant metadata in interoperable formats.
3. **Data Portability** — Users MUST be able to export their contributed data and migrate to compatible implementations without unreasonable technical restriction.
4. **Federated Continuity** — No implementation may impose centralized technical controls that prevent independent federation, self-hosting, or compatible forks.
5. **Governance Transparency** — Governance-affecting protocol changes MUST be publicly documented and versioned.
6. **Interoperability Preservation** — Extensions or enterprise features MUST NOT intentionally degrade interoperability with compliant implementations.

These invariants are normative and supersede conflicting implementation behavior.

### 3. Separate Protocol Layer from Application Layer

Without an architecture boundary, companies will ask "what exactly must stay open?" This generates adoption friction and legal uncertainty. The model:

```
Application Layer (closed OK)
 ├── UI, analytics, billing, enterprise tooling, private automation
        ↓
Protocol Layer (OCPL-protected)
 ├── identity formats
 ├── federation APIs
 ├── task schemas
 ├── governance messages
 ├── export formats
 └── interoperability rules
```

This is the most important future clarification. Without it, "open protocol" can coexist with a completely proprietary network in practice.

### 4. Tighten the "Enterprise Features" boundary

The current text permits "proprietary features on top of the open protocol core" but leaves the boundary fuzzy. An operator can keep the protocol technically open while moving all meaningful functionality into proprietary layers. Suggested language:

> "Core protocol interoperability and identity portability MUST remain available through open documented interfaces, regardless of what additional proprietary layers are offered."

Otherwise enterprise wrappers become effective capture through legal compliance.

### 5. Add a "No Hidden Dependencies" clause

A protocol can be "open" while secretly depending on closed embeddings, closed moderation APIs, hidden orchestration services, or proprietary identity resolvers. In the AI era this is a real risk:

> "Implementations MUST NOT require undisclosed proprietary services for protocol interoperability, identity verification, federation participation, or governance participation."

This prevents "open protocol, closed rails" from becoming the norm.

### 6. Define "Open Coordination Protocol" formally

The term is currently intuitive but legally fuzzy. A definition section should specify the criteria that make something a coordination protocol subject to OCPL:

- multi-party coordination
- interoperable implementations
- federated participation
- identity portability
- governance interaction
- machine-readable protocol state

Without this, OCPL risks being applied too broadly (all software) or too narrowly (only specific wire formats).

### 7. Formalize Identity Export guarantees

Identity Sovereignty is OCPL's signature differentiator. It deserves a minimum export guarantee definition:

- DID
- public keys
- attestations
- relationships / memberships
- governance history
- portable permissions

The concept: "export your digital citizenship." This is powerful and worth specifying with the same rigor as the 30-day / machine-readable-open-format requirement of Condition 3.

### 8. Add Explicit Anti-Embrace-Extend-Extinguish Protection

The single biggest practical threat to a protocol commons is the E3 pattern:

1. implement protocol
2. add proprietary extensions
3. dominate network effects
4. slowly fracture compatibility

Language needed:
- mandatory documentation of extensions
- extension interoperability (extensions MUST NOT break base protocol connectivity)
- protocol downgrade protection (compliant nodes MUST be reachable from extension-using nodes)

Matrix learned this lesson early. OCPL should build the protection in from v1.x.

### 9. Add AI/Agent Portability Clauses

Do not regulate AI behavior. Do protect:
- agent portability (agents are not locked to a specific inference provider)
- memory portability (agent memory is exportable in the same way as user identity)
- model replacement freedom

Suggested language:

> "An implementation MUST NOT technically restrict users from replacing AI models, agent runtimes, or inference providers used within the protocol."

This becomes enormous as agent ecosystems mature.

### 10. Add "Right to Exit" as a named principle

> "No compliant implementation may impose technical measures that unreasonably prevent users, communities, or federated nodes from migrating to compatible implementations."

This is anti-digital-feudalism in a single sentence. It deserves to be a named, citable principle rather than an implication of Conditions 2 and 3.

---

## Roadmap Suggestions

### RFC governance (do this before ecosystem growth)

The license text should remain compact. Technical definitions should evolve separately via a versioned RFC process:

```
RFC-0001 Constitutional Invariants
RFC-0002 Identity Portability
RFC-0003 Federation Model
RFC-0004 Capability Tokens
RFC-0005 Export Formats
RFC-0006 Hosted Source Rules
RFC-0007 Governance Transparency
RFC-0008 Agent Interoperability
```

This makes OCPL evolve like OCI, ActivityPub, Matrix, and Kubernetes APIs rather than becoming static legal text. The v1.0→v1.1 change (embedding invariants directly instead of referencing RFC 0001) was the right call for the core license; RFCs are the right home for the evolving technical definitions.

### Protocol Compliance Profiles

Not every project needs every clause. Modular profiles reduce adoption friction:

| Profile | Purpose |
|---------|---------|
| OCPL-Core | basic protocol openness + patent non-aggression |
| OCPL-Federated | federation guarantees |
| OCPL-Identity | DID portability |
| OCPL-Governance | voting / transparency |
| OCPL-Agent | AI agent interoperability |

### Reference Test Suites

A protocol license without compliance tooling becomes vague over time. The eventual goal:

```bash
ocpl verify
```

Checking: export capability, federation compatibility, API openness, identity portability, schema compliance. This moves OCPL from legal-only to technical ecosystem — the difference between a policy and an infrastructure standard.

### Badge / compliance signal system

Badges communicate compliance instantly and drive ecosystem adoption:

```
✓ OCPL-Core
✓ Federated
✓ Portable Identity
✓ Hosted Source
✓ Open Governance
```

### Neutral foundation (long-term)

If OpenKO alone controls OCPL permanently, ecosystem adoption will be limited by concerns about single-entity capture. The long-term model:

```
OpenKO Foundation (or OCPL Foundation or Protocol Commons Foundation)
 ├── RFC stewardship
 ├── trademark
 ├── compliance suites
 └── canonical definitions
```

Analogues: Linux Foundation, CNCF, W3C, Matrix.org Foundation. This does not need to happen at v1.x — but the governance structure should be designed so that the transition is possible without a license version bump.

---

## What to Avoid

**Anti-corporate language** — Legitimate commercial actors are necessary for ecosystem health. OCPL permits commercial activity deliberately. Keep language technical and constitutional, not adversarial.

**Moral / ethical language** — Vague principles ("for humanity," "non-harmful use") are unenforceable in most jurisdictions and create adoption barriers for legitimate uses. The Constitutional Invariants (Condition 5) are a better mechanism — they prohibit specific behaviors rather than restricting who can participate.

**Anti-AI language** — The protocol should be neutral on AI, with specific portability protections for users of AI-integrated implementations. The distinction is between protecting user rights (good) and restricting technology categories (bad).

**Copyleft propagation** — OCPL is not GPL. Propagating OCPL to linked code would make it unusable for commercial application layers built on top of OCPL infrastructure. The dependency boundary is essential and should be defended.

---

## Scale Vision

OCPL may eventually govern not just software licenses but agent societies, distributed research, knowledge commons, compute federations, autonomous organizations, and machine economies. The grounding insight is correct: OCPL is not primarily a software license — it is constitutional infrastructure for cooperative networks that include both humans and agents. The technical focus on interoperability, exportability, and governance continuity (rather than tokens or speculation) is what gives it a realistic path to that scope.
