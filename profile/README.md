<div align="center">

# Dove

**A family of dual-audience autonomous AI agents with verifiable per-decision provenance, each scoped to a regulated domain.**

*Open source · Apache-2.0 · Built on the [jhcontext-protocol](https://pypi.org/project/jhcontext-protocol/) substrate*

---

</div>

## What this is

Dove is the open-source reference implementation of an architectural pattern: a single named conversational agent that serves two audiences — one professional, one affected-by-decision — through distinct role-gated tools, with every tool invocation persisted as a signed envelope in an append-only provenance graph. The substrate makes each decision verifiable case-by-case under the regulation that governs its domain.

Three sister repositories, one per vertical, sharing a common Python substrate ([`jhcontext-sdk`](https://pypi.org/project/jhcontext-sdk/) + [`jhcontext-protocol`](https://pypi.org/project/jhcontext-protocol/)):

<table>
<tr>
<th align="left">Vertical</th>
<th align="left">Two audiences</th>
<th align="left">Regulatory anchor</th>
<th align="left">Status</th>
</tr>
<tr>
<td><b><a href="https://github.com/dove-agent/dove-edu-backend">dove-edu</a></b><br/>education</td>
<td>professors · students</td>
<td>EU AI Act Annex III §3<br/>GDPR Art 17</td>
<td>v0.1 scaffold ·<br/>backing the IJAIED 2026 paper</td>
</tr>
<tr>
<td><b>dove-health</b><br/>clinical decision support</td>
<td>clinicians · supervised reviewers<br/>(patient-facing surface in v2)</td>
<td>EU AI Act Annex III §5<br/>EU MDR Rule 11 · GDPR Art 9<br/>FDA SaMD · Brazilian CFM 2.314 / ANVISA RDC 657</td>
<td>proposal ·<br/>see <a href="https://github.com/dove-agent/.github/blob/main/proposals/dove-health.md">proposals/dove-health.md</a></td>
</tr>
<tr>
<td><b>dove-hire</b><br/>hiring &amp; assessment</td>
<td>recruiters · candidates</td>
<td>EU AI Act Annex III §4<br/>GDPR Art 22 · NYC LL144 · EEOC · Colorado AI Act</td>
<td>placeholder ·<br/>follows after dove-health</td>
</tr>
</table>

## The architectural commitment

Every Dove agent makes the same three structural promises by construction, not by deployment documentation:

1. **Dual-audience role separation.** A single named agent serves two audiences with asymmetric refusal contracts. The professional audience configures and reviews; the affected audience uses, contests, and queries provenance. The two audiences share exactly one artefact — the rubric in education, the clinical protocol in health, the assessment criteria in hiring — and every other artefact is single-audience-created with role-gated visibility.

2. **Per-decision evidence.** Every tool invocation, every internal handoff, and every model call produces a content-hashed signed envelope persisted to an append-only provenance graph (W3C PROV under the hood). The graph is queryable by the affected person — directly through the agent, not through the deployer's logs — for the right-to-explanation that the relevant regulation requires.

3. **Structural verifiers.** A small set of SDK-provided verifiers (`verify_integrity`, `verify_temporal_oversight`, `verify_pii_detachment`, `verify_negative_proof`, `verify_workflow_isolation`, plus domain-specific extensions) consume the provenance graph and produce typed pass/fail outputs. The verifier output is the per-decision answer to "was this decision made the way the regulation requires?"

## Companion papers

| Vertical | Paper | Venue | Status |
|---|---|---|---|
| dove-edu | *"Dove: The Rubric as Shared Contract — An Auditable Autonomous AI Agent for Professors and Students"* | International Journal of Artificial Intelligence in Education (IJAIED, Springer / Elsevier from Jan 2026) | Draft |
| dove-health | TBD — see [proposals/dove-health.md](https://github.com/dove-agent/.github/blob/main/proposals/dove-health.md) | npj Digital Medicine (Nature) — primary target; JAMIA or Artificial Intelligence in Medicine as fallback | Proposal |
| dove-hire | TBD | ICIS / Information Systems Research — Responsibility and Ethics track | Roadmap only |

The IJAIED paper introduces the architectural pattern in detail; the dove-health and dove-hire papers will be sibling instantiations.

## Substrate and dependencies

Each Dove imports the [PAC-AI](https://pypi.org/project/jhcontext-protocol/) substrate from PyPI rather than vendoring it: `jhcontext-sdk` provides envelopes, the PROV graph builder, the ForwardingEnforcer, and the structural verifiers; `jhcontext-protocol` provides the wire-level envelope schema. Keeping the substrate as a versioned PyPI dependency means improvements to one Dove improve all three.

## Get involved

- **Read the IJAIED paper** (link added when accepted) for the full architecture and use-case walk-through.
- **Clone [dove-edu-backend](https://github.com/dove-agent/dove-edu-backend) and [dove-edu-frontend](https://github.com/dove-agent/dove-edu-frontend)** for the reference implementation; both run locally against LocalStack and deploy cleanly to AWS + Vercel.
- **File an issue on the relevant repo** with the vertical tag (`edu`, `health`, `hire`) — design discussions, regulatory questions, and verifier proposals all welcome.
- **Pitch a new vertical** by opening a discussion on this repo. The current shortlist beyond the three above includes `dove-finance` (lending decisions under FCRA / DORA), `dove-housing` (tenant screening under Fair Housing Act), and `dove-immigration` (visa adjudication assistance). The architectural pattern transfers wherever a regulated decision affects an identifiable person and a regulator wants per-decision evidence.

## Licence

Code: **Apache-2.0** across all repositories.
Brand assets (logo, illustrations): **CC BY 4.0**, in each repo's `brand/` folder.

---

<div align="center">

*Maintained by [João Henrique da Rosa](https://github.com/jhcontext) and contributors.*

</div>
