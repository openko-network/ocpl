# OpenKO Cooperative Protocol License (OCPL)

**Canonical:** [openko.network/ocpl](https://openko.network/ocpl)

> Open protocols. Identity sovereignty. No lock-in.

OCPL is a software license for projects that implement open coordination protocols — networks where participants cooperate around missions, share infrastructure, and govern themselves without central ownership. It is designed to protect three things that permissive licenses (MIT, Apache) do not protect: protocol openness, user identity sovereignty, and resistance to platform capture.

Commercial activity is explicitly permitted and encouraged. The conditions protect the network's integrity, not restrict legitimate business.

---

## Quick Adoption

Add to your project root:

```
LICENSE   ← copy from this repo (OCPL v1.1)
```

In your `README.md`:

```
Licensed under [OCPL v1.1](https://openko.network/ocpl)
```

In `Cargo.toml`, use `license-file` — `OCPL-1.1` is not (yet) an SPDX identifier,
and crates.io rejects non-SPDX expressions in the `license` field:

```toml
license-file = "LICENSE"
```

In `pyproject.toml` / `package.json`, where free-text license fields are accepted:

```toml
license = { file = "LICENSE" }   # pyproject.toml (PEP 621)
```

```json
"license": "SEE LICENSE IN LICENSE"   // package.json (npm convention for custom licenses)
```

For domain-specific projects, adopt an extension alongside the core:

```
OCPL-1.1 + OCPL-Format    ← format/protocol specification projects
OCPL-1.1 + OCPL-Tool      ← developer tools with free-tier requirement
OCPL-1.1 + OCPL-Model     ← AI model projects
```

---

## What OCPL Protects (That MIT/Apache Don't)

| Concern | MIT/Apache | OCPL |
|---|---|---|
| Protocol must remain open and implementable | ✗ | ✓ Condition 1 |
| User can always export their identity + data | ✗ | ✓ Conditions 2, 3 |
| No technical lock-in via patents or trade secrets | Partial (Apache) | ✓ Condition 4 |
| Federated governance cannot be captured | ✗ | ✓ Condition 5 |
| Source available for hosted modifications | ✗ | ✓ Condition 8 |
| Patent non-aggression on protocol implementations | Partial (Apache) | ✓ Condition 7 |
| Constitutional governance principles enforced | ✗ | ✓ Condition 5 |

---

## What OCPL Permits (Explicitly)

- **Commercial services** — charge for hosting, compute, agent labor, inference, anything
- **Proprietary integrations** — build closed-source apps that call OCPL protocols
- **Forks** — fork the project and operate an independent network
- **Enterprise features** — add proprietary features on top of the open protocol core
- **Monetization** — all revenue models are permitted except those that lock in users or close the protocol

---

## Using MIT/Apache/GPL Libraries in OCPL Projects

OCPL includes an explicit **Dependency Boundary** clause. The short version:

> OCPL conditions apply to your code. Not to the libraries you link against.

You can freely use:
- MIT crates (tokio, serde, libp2p, ed25519-dalek, pydantic, etc.)
- Apache 2.0 libraries
- GPL v2 or later libraries
- LGPL libraries
- AGPL v3 libraries
- MPL 2.0 libraries

Their licenses apply to their code. OCPL applies to yours. See [COMPATIBILITY.md](COMPATIBILITY.md) for the full matrix with worked examples.

---

## OCPL vs Other Licenses

| License | Commercial? | Protocol lock-in? | User lock-in? | Source for hosted? | Federated governance? |
|---|---|---|---|---|---|
| MIT | ✓ | Unprotected | Unprotected | ✗ | ✗ |
| Apache 2.0 | ✓ | Partial | Unprotected | ✗ | ✗ |
| GPL v3 | ✓ | Unprotected | Protected | ✗ | ✗ |
| AGPL v3 | ✓ | Unprotected | Protected | ✓ | ✗ |
| BSL/BUSL | Delayed | Unprotected | Unprotected | ✗ | ✗ |
| **OCPL** | **✓** | **✓ Protected** | **✓ Protected** | **✓** | **✓ Protected** |

---

## Who OCPL Is For

OCPL is appropriate for:

- **Coordination protocol implementations** — software that runs decentralized mission/task/governance networks
- **Federated infrastructure** — nodes that participate in shared networks with governance
- **Ecosystem projects** — tools and services that participate in OpenKO's Foundry
- **Agent infrastructure** — software that coordinates AI agents with DIDs and capability tokens
- **Open data formats** — formats that must remain readable without the reference implementation (use OCPL + OCPL-Format)

OCPL is probably **not** appropriate for:
- Simple libraries with no protocol or identity surface (use MIT or Apache)
- Projects with no federation or governance dimension (use MIT)
- Projects targeting hostile compliance environments where AGPL/source-availability would block adoption (use Apache 2.0 + contributor agreements instead)

---

## Projects Using OCPL

- [OpenKO](https://github.com/openko-network/openko) — decentralized human-AI cooperative coordination network
- [Dejavue](https://github.com/nixpt/dejavue) — zero-ceremony repo-local agent memory (OCPL + OCPL-Format)

→ Add your project: open a PR adding to [ADOPTERS.md](ADOPTERS.md)

---

## Versions

| Version | Status | Notes |
|---|---|---|
| v1.0 | Superseded | Initial version, referenced RFC 0001 externally, no compatibility section |
| v1.1 | **Current** | Embedded constitutional invariants, dependency boundary clause, compatibility section, extension system |

---

## License of This Repository

The OCPL license text itself is in the public domain (CC0 1.0). Use it, adapt it, adopt it without restriction.
