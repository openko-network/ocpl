# OCPL-Format Extension

**Version:** 1.0  
**Applies to:** Format specification projects — software that defines an on-disk or wire format that other tools must be able to consume independently.  
**Use alongside:** OCPL v1.1 core (this extension adds conditions; it does not replace core conditions)

**Declaration:** `OCPL-1.1 + OCPL-Format-1.0`

---

## Additional Conditions

The following conditions apply in addition to all OCPL v1.1 core conditions.

### F1. Format Openness

The on-disk or wire format defined by this software must remain publicly documented in a form that allows any developer to implement a compatible reader or writer without access to this software's source code or binary.

You may not:
- Move the format specification behind authentication, paywalls, or access controls
- Introduce undocumented fields or encoding tricks that are required for correct parsing
- Use obfuscation, encryption, or compression (without documented decompression) to make the format unreadable without this software

You may:
- Add new documented fields in a versioned, backward-compatible way
- Define optional extensions that are clearly marked as optional in the spec
- Provide reference implementations in any language

### F2. Format Portability

Any hosted service operating this software must, upon user request, export all data in the canonical format defined by the format specification — not in a proprietary derivative. The export must be usable without this software.

### F3. Format Lineage

The format specification version history must be publicly maintained. Users and implementors must be able to determine what any format version contains and how it differs from prior versions. Specifications may not be retroactively amended to change the semantics of already-published versions.

### F4. Independent Implementability

The conditions of this license, and the format specification itself, must make it possible for a third party to write a fully compliant reader and writer without accessing this software's source code. If the format requires cryptographic operations, the algorithms must be documented using public standards (e.g., RFC-referenced algorithms), not proprietary schemes.

---

## Example: Dejavue

Dejavue (`github.com/nixpt/dejavue`) adopts OCPL-1.1 + OCPL-Format-1.0. The `.dejavue/` on-disk format (timeline.jsonl, decisions.md, state.md, handoff.md, references/) is the open contract:

- Any tool can read `.dejavue/` without the dejavue CLI
- The format is documented in the repository
- Other agents (Cursor, Aider, opencode) can consume the format directly
- A hosted dejavue-server must export memory in the `.dejavue/` canonical format

This extension formalizes that commitment in the license.

---

## Declaration in foundry.toml

```toml
[project]
license = "OCPL-1.1+Format"

[capabilities]
contributes = ["knowledge.memory"]

[economics.royalties]
# Optional: register format dependency for attribution CU routing
format_dependency = "my-project.format:1.0"
```
