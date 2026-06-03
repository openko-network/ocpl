# OCPL — Frequently Asked Questions

---

**Can I use MIT/Apache libraries in my OCPL project?**

Yes. OCPL includes an explicit Dependency Boundary clause. MIT and Apache libraries stay under their own licenses; your OCPL code stays under OCPL. This is the same pattern as using MIT libraries in an Apache project.

---

**Can I build a closed-source product on top of OCPL software?**

Yes. You can build proprietary applications, services, and integrations on top of OCPL infrastructure. What you cannot do is close the protocol itself, lock in users, or modify the OCPL core without releasing those modifications if you run a public hosted service. Application-layer code is yours to keep proprietary.

---

**Can I charge for my OCPL software or service?**

Yes, explicitly. OCPL Permissions section (e) grants the right to "charge for services, hosting, compute, agent labor, resource access, and any other commercial activity built on top of this software." The conditions protect users and the protocol; they do not restrict commercial activity.

---

**Does OCPL require me to release my source code?**

Only if you run a public hosted service using a **modified** version of the OCPL software (Condition 8 — Source Availability for Network Services). If you: (a) run the software unmodified, (b) use it internally only, or (c) build proprietary application code on top without modifying the OCPL core — no source release is required.

---

**Is OCPL compatible with GPL v3?**

Yes. GPL v3 §7 allows additional terms that are user-protective, which OCPL's conditions are. OCPL Condition 8 is compatible with AGPL §13 (the network service source availability requirement). See [COMPATIBILITY.md](COMPATIBILITY.md) for the worked example.

---

**Can I use GPL v2 libraries in my OCPL project?**

Use caution. GPL v2's "no further restrictions" clause may conflict with OCPL Condition 5. Most GPL v2 projects are actually "v2 or later" — if so, treat them as GPL v3 where the conflict does not apply. For GPL v2-only libraries, review the specific terms or avoid them in the protocol core.

---

**Does OCPL propagate to software that uses my OCPL library?**

No. OCPL is not copyleft in the GPL sense. The Dependency Boundary clause explicitly states that OCPL applies only to the covered work, not to software that links against it. Software using an OCPL library does not become OCPL.

---

**Can I fork an OCPL project and add proprietary features?**

Yes. You can fork, add proprietary application-layer features, and operate commercially. You must: (a) keep the protocol open and interoperable, (b) not lock in users, (c) preserve the constitutional invariants, (d) release modifications to the OCPL core if you run a public hosted service. Application-layer additions are yours.

---

**What is the difference between OCPL and AGPL?**

AGPL prevents the "hosted service" loophole in GPL: if you run GPL software as a service, AGPL requires you to provide source to users. OCPL does the same (Condition 8) but adds protocol-specific protections that AGPL does not: interoperability requirements, user identity sovereignty, no lock-in, and constitutional governance invariants.

---

**What are the "constitutional invariants" in Condition 5?**

Ten principles that the software must enforce and that cannot be removed through modification. They include: no permanent central authority, open protocols, voluntary participation, transparent contributions, identity sovereignty, portable knowledge, federated governance, auditable AI systems, local autonomy, and public-good mission prioritization. See [RATIONALE.md](RATIONALE.md) for why each exists.

---

**Can I adopt OCPL for a project that isn't part of the OpenKO ecosystem?**

Yes. OCPL is a general-purpose license for coordination protocol software. It does not require participation in the OpenKO network or Foundry. If your project implements open coordination protocols and you want the protections OCPL provides, adopt it.

---

**What is the difference between OCPL-1.0 and OCPL-1.1?**

OCPL v1.0 had three problems: it referenced external documents (RFC 0001) that could change, it used vague language ("canonical repository"), and it had no compatibility or dependency boundary sections. OCPL v1.1 fixes all three: embeds the constitutional invariants directly, clarifies the dependency boundary explicitly, and adds a compatibility section. See [versions/v1.0.md](versions/v1.0.md) for the original text.

---

**What are OCPL extensions?**

Named additional conditions for domain-specific projects:
- **OCPL-Format**: for format/protocol specification projects (open format guarantee)
- **OCPL-Tool**: for developer tools (free local CLI tier requirement)
- **OCPL-Model**: for AI model projects (weight availability, training data lineage)

Extensions add conditions; they cannot remove core OCPL conditions. See [extensions/](extensions/).

---

**What is the license of the OCPL text itself?**

CC0 1.0 (public domain). You may use, adapt, and adopt the OCPL text for your own license without restriction or attribution.

---

**How do I report a compliance violation?**

File an issue at https://github.com/nixpt/ocpl/issues. For urgent or sensitive matters (active user lock-in, patent threats), contact the OpenKO governance council at the address in the OpenKO repository.
