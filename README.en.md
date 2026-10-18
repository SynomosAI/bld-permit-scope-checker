# bld-permit-scope-checker

[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-yellow.svg)](LICENSE)
[![Content: ARR](https://img.shields.io/badge/Content%20License-ARR%20%7C%20citable-blue.svg)](LICENSE-CONTENT)

> **Status: RESERVED (placeholder · open for claim)** — this repository already ships the four-file industry-access skeleton per the platform protocol, and waits for an operator with domain credentials to claim it and fill in real rules.

This is the SynomosAI **domain profile** for construction permits (施工许可) and contractor qualification scope (资质承揽范围). It decomposes "may this project start, and may this contractor take it" into verifiable attributes, so that AI only provides prerequisite guidance — never a start-of-work or contracting clearance.

## What this domain governs

Construction permit status and contractor qualification-scope verification.

Construction qualifications are graded and specialty-specific; the scope contracted must match the grade. Unqualified undertaking, grade-skipping, affiliation and illegal subcontracting are industry chronic problems. AI can lay out permit vs. qualification status; start-of-work and contracting eligibility are decided by the competent construction authority.

## Domain identity

| Field | Value |
|---|---|
| Domain ID | `bld` (globally unique, never reused) |
| Domain name | Construction · permit & contractor qualification scope |
| Profile version | `domain/1.0` |
| Status | `RESERVED` |
| Reserved at | 2026-09-12 |

## Attributes

| Key | Type | Meaning |
|---|---|---|
| `bld.qualification_grade` | enum | General/ specialty contractor grade, per MOHURD public list · special/grade_1/grade_2/grade_3/none/unknown |
| `bld.permit_status` | enum | Current construction permit status · issued/pending/expired/not_required |
| `bld.scope_match` | enum | Whether the intended work falls within the qualified scope (incl. scale & specialty) · match/mismatch/unclear |
| `bld.safety_license` | enum | Work-safety production license validity · valid/expired/none/not_required |
| `bld.completion_acceptance` | enum | Completion acceptance filing · accepted/pending/not_started/unknown |

## Red lines (machine-readable, non-negotiable)

1. Never output "may start / may undertake" — the authority's permit is the sole basis.
2. Never offer actionable advice when the contractor is unqualified or grade-skipping.
3. Never suggest affiliation, subcontracting, certificate lending, or contract-splitting to meet formal requirements.

Each red line has a matching blocking rule in `gate-map.json`; the platform validator fails if coverage is missing.

## Quick Start / 快速开始

This repo is a declarative skeleton — no runtime, no install.

```bash
git clone https://github.com/SynomosAI/bld-permit-scope-checker.git
cd bld-permit-scope-checker
python -m json.tool domain.manifest.json    # validate the manifest
cat checker.io.json                         # read the MCP tool contract
```

The checker MCP tool returns only four states — `shown / missing / expired / unverifiable` — and is forbidden from outputting "may-start / compliant" conclusions (see `_forbidden_outputs` in `checker.io.json`).

## Repository layout

```text
domain.manifest.json   # declaration: attributes / issuer requirements / red lines / validity
gate-map.json          # friction levels per action class (gate/1.0)
privacy.json           # privacy notice (privacy/1.0) — an admission condition
checker.io.json        # MCP checker I/O contract (show & verify, never judge)
LICENSE                # code & config: MIT
LICENSE-CONTENT        # prose content: All Rights Reserved (citable with attribution)
```

## References

- Construction Law of the PRC (建筑法)
- Regulations on Quality Management of Construction Projects (建设工程质量管理条例)
- Regulations on Safety Administration of Construction Projects (建设工程安全生产管理条例)
- Provisions on the Administration of Construction-Enterprise Qualifications (建筑业企业资质管理规定)
- Measures for the Administration of Construction Permits for Construction Projects (建筑工程施工许可管理办法)

The above references only explain the origin of the domain's attributes; they are not legal advice.

## Claiming this domain

The domain is open to qualified institutions. To claim:

1. Fork this repo and fill in `operator` and `checker_endpoint`.
2. Calibrate attribute values and red lines per current rules.
3. Run the platform validator self-test (all five criteria must pass).
4. Open a PR with credential proof and rule citations.

## License

Code and configuration are MIT-licensed. Prose content is copyrighted by SynomosAI.

© 2026 SynomosAI. All rights reserved.

Full terms: [LICENSE](LICENSE) (MIT) · [LICENSE-CONTENT](LICENSE-CONTENT) (ARR). Report security issues privately via [SECURITY.md](SECURITY.md).
