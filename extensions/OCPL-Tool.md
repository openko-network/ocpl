# OCPL-Tool Extension

**Version:** 1.0  
**Applies to:** Developer tooling — CLI tools, IDE extensions, agent frameworks, and other software used directly by developers where a free local tier is essential for adoption and trust.  
**Use alongside:** OCPL v1.1 core  
**Declaration:** `OCPL-1.1 + OCPL-Tool-1.0`

---

## Additional Conditions

### T1. Free Local Tier

The local command-line interface or local execution mode of this software must remain available at no charge (no CU, no subscription, no API key required) for standard operations.

"Standard operations" includes: initialization, local capture (decisions, notes, state, handoff), local recall (keyword and semantic search over local data), context boot packets, and any operations that work without network connectivity.

Monetization may apply to:
- Hosted services (cloud execution, shared team memory, managed APIs)
- Capsule or server deployments
- Enterprise features (SSO, CI integration, compliance archival, cross-organization federation)
- API rate tiers above a reasonable free baseline

Monetization may NOT apply to:
- The core local tool itself
- Operations that work offline without the hosted service

### T2. Offline Capability

The core operations of this software must remain functional without network connectivity. A user must be able to run the tool on an air-gapped machine for their local data. Network-dependent features may require network access; the local core may not.

### T3. No Telemetry Without Consent

This software must not transmit usage data, telemetry, or error reports to any remote server without explicit, informed opt-in from the user. Opt-in must be:
- Presented at first use (not buried in terms of service)
- Reversible at any time without losing functionality
- Clearly labeled with what data is transmitted and to whom

---

## Example: Dejavue

Dejavue adopts OCPL-1.1 + OCPL-Tool-1.0:
- The dejavue CLI is free — 36 commands, no API key, no account
- All local operations (init, decision, state, handoff, context, recall) work offline
- Hosted dejavue-server is paid (monetization applies to the service, not the tool)
- No telemetry is transmitted from the local CLI

---

## Declaration in foundry.toml

```toml
[project]
license = "OCPL-1.1+Tool"

[economics.modes]
cli_mode     = "free"        # required by OCPL-Tool
primary_mode = "hosted-service"
```
