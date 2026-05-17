# dove-health — proposal

This document sketches what `dove-health` is, why the dove-edu pattern *partly* transfers and *partly* doesn't, what to build first, and where to submit the companion paper. It draws on the architectural lessons in [dove-edu](https://github.com/dove-agent/dove-edu-backend) (this org) and on two PAC-AI healthcare papers in the author's portfolio: the [AIiH 2026 protocol paper](https://github.com/jhcontext/jhcontext-papers/tree/main/aiih) (12pp LNCS, PAC-AI multi-agent clinical governance, three scenarios) and the [AIiH 2026 Special Session cross-jurisdictional taxonomy](https://github.com/jhcontext/jhcontext-papers/tree/main/aiih_star) (24pp LNCS, 12 functional categories × 3 audiences × 3 jurisdictions, 5 anchor incidents).

## What dove-health is — and what it deliberately is not

dove-health is the **clinician-led** dove. A clinician authors and publishes a clinical protocol (the analog of dove-edu's rubric); a downstream agent (Dove) applies that protocol to a specific patient case under the clinician's continuous oversight; a second clinician (the supervisor or remote specialist) reviews and commits the decision; the patient gets a per-decision provenance package she can carry to a contestation procedure if she disagrees.

**The shared contract is not a rubric**. The clinician–patient relationship is fiduciary, not pedagogical, so the dove-edu pattern of *transparent success criteria the student is tutored toward* does not transfer cleanly. The PAC-AI healthcare papers already give the right substitute: the **clinical protocol + the `feature_suppression` array** in the envelope semantic payload. The protocol declares what the agent will and will not consider; the `feature_suppression` array makes the negative explicit ("this decision did not consider race, postcode, insurance status, prior denials, …"). Together they document the *contract the clinician published* — visible to the patient, queryable, contestable.

**The two audiences are not symmetric the way they are in dove-edu**. In dove-health v1, the two roles are **clinician** (primary) and **supervised reviewer** (specialist or second clinician), not clinician and patient. The patient is an *affected person with statutory rights* (EU AI Act Art 86 right to explanation, GDPR Art 22 right to human review), but she is not a user of the agent. v2 introduces a **patient-facing surface** for the provenance-query right; that step crosses an EU AI Act / FDA regulatory threshold (Art 50 transparency-to-lay-users + patient-facing CDS classification) and should not be attempted in v1.

**dove-health is not a diagnostic device**. v1 stays inside the Cures Act §3060 CDS exemption (US) and Class IIa equivalent (EU) by ensuring the clinician retains decision authority and can independently review the basis. Whether v2 crosses into Class IIb / SaMD II is a regulatory decision made when v1 is mature, not a starting position.

## Architecture sketch

The seven dove-edu tools become a seven-tool dove-health surface with a near-identical shape:

| dove-edu tool | dove-health analog | Audience | Crew |
|---|---|---|---|
| `build_rubric` | `build_protocol` | clinician | `ProtocolBuilderCrew` |
| `publish_rubric` | `publish_protocol` | clinician | — |
| `commit_grade` | `commit_decision` | clinician | — |
| `tutor_me` | `consult_for_patient` | clinician | `ConsultationCrew` |
| `submit_draft` | `submit_case` | clinician (NOT patient) | `CaseEvaluatorCrew` |
| `query_my_provenance` | `query_case_provenance` | patient (via clinician-issued token) OR auditor | — |
| `delete_my_data` | `delete_case_data` | patient OR clinician | — |

Note that `submit_case` is **clinician-initiated** in v1 (the clinician submits a case for AI-assisted evaluation; the patient is not a user). The patient's relationship with the agent is exclusively via `query_case_provenance` after a decision has been committed.

The three crews change as follows:

| dove-edu crew | dove-health crew | Internal agents |
|---|---|---|
| RubricBuilderCrew | **ProtocolBuilderCrew** | `ProtocolTemplateAdvisor` (recommends among care-plan / triage-protocol / decision-support-script / monitoring-rule), `FeatureSuppressionElicitor` (negotiates what the agent will and will not consider), `ProtocolValidator` (regulatory-fit + audit-defensibility check) |
| TutorCrew | **ConsultationCrew** | `EvidenceRetriever` (FHIR / EHR query), `ProtocolApplier` (per-step application of the published protocol), `RiskCalibrator` (flags case-protocol mismatches) |
| EssayEvaluatorCrew | **CaseEvaluatorCrew** | `IdentityBlindReader` (PII-detached case summary), `ProtocolMatcher` (applies the published protocol), `EvidenceFinder` (cites the FHIR resources that grounded each recommendation), `Calibrator` (cross-recommendation consistency + `verify_negative_proof` against the `feature_suppression` array), `Auditor` (Ed25519-signs the envelope chain) |

Five structural verifiers (the dove-edu set) all carry over directly:

- `verify_integrity` — content-hash + signature chain
- `verify_temporal_oversight` — the supervised-reviewer activity occurred after the AI output and before the decision commit
- `verify_pii_detachment` — patient identity tokenised before any crew runs
- `verify_negative_proof` — the `feature_suppression` array is honoured (no suppressed feature appears anywhere in the case PROV graph)
- `verify_workflow_isolation` — separate cases share no entities

Two new dove-health-specific verifiers:

- **`verify_protocol_grounding`** — every recommendation in the AI output binds to a specific clause of the published protocol with a cited FHIR resource
- **`verify_dual_review_for_high_risk`** — for decisions classified high-risk (per the protocol's own risk tier), the PROV graph shows a second clinician's review activity, not just the primary clinician's commit

## Persistence and substrate

The substrate is the same: `jhcontext-sdk` + `jhcontext-protocol` from PyPI, identical envelope schema, identical PROV graph builder, identical ForwardingEnforcer with `semantic_forward` / `raw_forward` policies. The DAOs add one (`ProtocolDao` replaces `RubricDao`), promote `PiiTokenDao` to higher-grade encryption (separate per-tenant KMS CMK, shorter TTL, mandatory audit-trail on every reattachment), and add `ConsentDao` (records the patient's explicit consent for AI-assisted evaluation, the legal basis under GDPR Art 9(2)(h) or 9(2)(a), and the revocation history).

The deployment shape is also the same — Chalice REST + WSS on AWS Lambda, CrewAI worker on Lambda container, DynamoDB persistence, Vercel frontend — with two production-grade adjustments: (a) the API runs in a HIPAA-eligible AWS region with a signed Business Associate Agreement; (b) the LLM provider adapter is restricted at deploy time to providers with HIPAA-eligible offerings (Anthropic, Azure OpenAI; Gemini's HIPAA status varies). The user-supplies-their-own-key pattern remains, but the system refuses to start in patient-data mode unless the supplied key is a HIPAA-eligible one.

## Regulatory anchors per scenario

dove-health v1 should land in three or four scenarios that mirror the dove-edu scenarios A–E, with the regulation each scenario discharges baked into the §6 walkthrough:

| dove-health scenario | EU AI Act | EU MDR | GDPR | US (HIPAA/FDA) | UK (DCB/MHRA) | Brazil (CFM/ANVISA/LGPD) |
|---|---|---|---|---|---|---|
| A — Clinician authors + publishes a protocol | Art 13 | Rule 11 | Art 5 minimisation | HIPAA 164.512(b) | DCB0129 | CFM 2.314 Art 4 |
| B — Clinician consults dove during a patient encounter | Art 13, 15 | — (CDS exemption applies if clinician retains authority) | Art 6 legal basis | Cures Act §3060 | NHS DTAC | CFM 2.314 Art 7 |
| C — dove evaluates a case the clinician submitted | Art 12, 15 | Rule 11 Class IIa | Art 9(2)(h) special category | HIPAA + Cures §3060 | DCB0160 | ANVISA RDC 657 |
| D — Supervisor reviews and clinician commits the decision | Art 14 | — | — | — | DCB0129/0160 | CFM 2.314 Art 6 |
| E — Patient queries the provenance of her case | Art 86 | — | Art 22 | HIPAA 164.524 access | UK GDPR Art 22 | LGPD Art 11 + Art 20 |

The cross-jurisdictional taxonomy in [aiih_star §4](https://github.com/jhcontext/jhcontext-papers/blob/main/aiih_star/sections/04taxonomy.tex) is exactly the right anchor for this scenario table — for each scenario, the same regulatory cell across 3–4 jurisdictions is named and cited. This is the **single most differentiated thing** about a dove-health paper relative to the existing PAC-AI healthcare papers: dove-edu is single-jurisdiction (EU AI Act-only); dove-health goes cross-jurisdictional by construction.

## What's NEW vs. what builds on PAC-AI healthcare prior work

The author's [AIiH 2026 protocol paper](https://github.com/jhcontext/jhcontext-papers/tree/main/aiih) and [AIiH 2026 cross-jurisdictional taxonomy](https://github.com/jhcontext/jhcontext-papers/tree/main/aiih_star) already establish:

- PAC-AI envelopes + structural verifiers in a clinical context (aiih §3)
- Three clinical scenarios with EU AI Act mapping (aiih §5)
- Cross-jurisdictional taxonomy of 12 functional categories × 3 audiences × 3 jurisdictions (aiih_star §4)
- Per-incident gap analysis against 5 anchor incidents (aiih_star §7)
- Multi-agent frontier discussion (aiih_star §8)

dove-health is **NEW work** on top of those, adding:

1. **A named dual-audience agent** (Dove-as-clinician's-consultant) with a published refusal contract, role-aware tool surface, and a single open-source reference implementation. The PAC-AI healthcare papers describe the substrate; dove-health describes a *product* built on it.
2. **The protocol-as-shared-contract pattern** ported from dove-edu, with the `feature_suppression` array as the technical realisation. PAC-AI describes the field; dove-health makes it the load-bearing structural commitment.
3. **The patient-facing provenance-query surface** (Scenario E), which neither AIiH paper develops — the AIiH papers are clinician-only.
4. **Brazil compliance** (CFM 2.314 + ANVISA RDC 657 + LGPD), which both AIiH papers explicitly defer. dove-health closes that gap.
5. **An open-source implementation** with a hosted demo any reader can exercise — the AIiH papers are protocol-and-scenario specifications, not products.

## Target venues

Three candidates, ranked by my recommendation.

### 1. *npj Digital Medicine* (Nature) — primary target

Open-access; impact factor ~15; turnaround 2–6 months; acceptance rate ~10%. **Strongest fit** because:

- They have published cross-jurisdictional governance papers (Aboy et al. 2024 on EU AI Act for digital medical products; Balogun et al. 2024 on EU AI Act + MDR integration — both already cited in the AIiH papers)
- They welcome **implementation papers backed by an open-source artefact and a live demo**
- They want clinical-AI papers that say something honest about regulation; dove-health's per-decision-evidence framing is unusual enough to land
- Article-processing-charge is paid by Nature's open-access framework; the author's institution may have a transformative agreement that covers it

**Risk:** desk-rejection rate is high. The cover letter and abstract have to lead with the architectural contribution, not the engineering work.

### 2. *Journal of the American Medical Informatics Association* (JAMIA) — strong fallback

Open-access option; impact factor ~5; turnaround 3–9 months; acceptance rate ~25%. **Strong fit** because:

- JAMIA loves clinical-decision-support governance papers and routinely publishes architectural pattern work
- Their reviewer pool understands FHIR + AI + workflow integration — fewer of the basic regulatory questions a generalist journal would raise
- The dove-health Brazil compliance angle reads well in JAMIA's "global-health informatics" track

**Risk:** less impact than npj Digital Medicine; the cross-jurisdictional framing might be considered too niche.

### 3. *Artificial Intelligence in Medicine* (Elsevier) — broader-scope fallback

Hybrid open-access; impact factor ~7; turnaround 3–8 months; acceptance rate ~20%. **Good fit** because:

- Broad scope (technical AI + clinical workflow + governance all welcome)
- Solid track record on multi-agent + provenance + compliance papers
- Reviewer pool is technically deeper; the structural-verifier work will land well

**Risk:** the editorial line tilts technical; the dual-audience / patient-rights framing may be considered out-of-scope and editor-redirected to a health-policy journal.

**My recommendation:** target *npj Digital Medicine* with a 6,000-word manuscript + an extensive open-source artefact + a hosted demo. Prepare a JAMIA-formatted backup so a desk-rejection at npj can be turned around in two weeks rather than two months.

### Conferences worth considering instead / alongside

- **AMIA Annual Symposium** (US, November; submission June). Strong on clinical informatics + governance; would be a good *complement* to the journal paper rather than a substitute.
- **MIE (Medical Informatics Europe)** (Europe, May; submission January). Right venue for the EU AI Act + MDR framing specifically.
- **AIiH 2027** (Imperial College London, summer 2027). Author already has portfolio there; dove-health would be a natural extension of the AIiH 2026 papers and could form a three-paper arc.

## Roadmap

| Phase | What | Status |
|---|---|---|
| 0 | This proposal | done (2026-05-17) |
| 1 | Scaffold `dove-health-backend` and `dove-health-frontend` (mirror dove-edu) | not started |
| 2 | Implement `build_protocol` + `publish_protocol` + `ProtocolBuilderCrew` as the v1 walking skeleton | not started |
| 3 | Draft the dove-health paper §1–§4 (intro, background, related, architecture) | not started |
| 4 | Implement `submit_case` + `CaseEvaluatorCrew` against three reference scenarios (e.g. ED triage, dermatology referral, COPD exacerbation monitoring) — one Brazil-specific to anchor the LGPD/CFM/ANVISA contribution | not started |
| 5 | Hosted demo + replication package | not started |
| 6 | Draft §5–§8 of the paper + submit to npj Digital Medicine | not started |
| 7 | Patient-facing provenance-query surface (v2 — regulatory-threshold-crossing; do not start until v1 is stable) | future |

## Open questions

1. **Is the clinician-led v1 too cautious?** A bolder v1 would put the patient in the loop earlier (e.g. patient consents to a specific protocol, clinician then operates within that consent). But that crosses Art 50 transparency obligations and risks SaMD II classification before the architecture is proven.
2. **Brazil-first or EU-first?** The biggest *novelty* relative to the AIiH papers is the Brazil integration. But EU-first has the larger immediate audience. A possible hybrid: EU as the primary scenario set, Brazil as a discussion-section bridge with a single worked LGPD/CFM example.
3. **Which three clinical scenarios?** The aiih paper has acute / longitudinal / task-shifted. dove-health could either reuse those or pick three *named-condition* scenarios (sepsis, melanoma triage, hypertensive crisis) that give the paper concrete clinical specificity and named-comparator positioning.
4. **Where does Vorrai end and dove-health begin?** Vorrai's clinical-receptionist wedge is admin-only by design (no health data). dove-health is *not admin-only*. The two are sibling brands with deliberately different scopes — the Vorrai wedge is a **route to market**, dove-health is a **research-and-OSS surface**. Keep the brand boundary explicit in any joint communication.
