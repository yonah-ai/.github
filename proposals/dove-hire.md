# dove-hire — placeholder

This is a one-page placeholder so the org `README` and `profile/README.md` can link somewhere coherent. The full proposal will be drafted **after dove-health v1 is published** — the dove-health paper will validate the dual-audience pattern in a regulated domain that is genuinely fiduciary, and the lessons from that validation should shape the dove-hire design before any code is written.

## What dove-hire will be

A dual-audience autonomous AI agent for hiring and assessment:

- **Recruiter audience** authors and publishes assessment criteria (the analog of dove-edu's rubric and dove-health's clinical protocol), reviews AI-shortlisted candidates, commits hire / reject decisions.
- **Candidate audience** queries the per-decision provenance of any assessment they were subject to — what criteria were applied, which CV / interview / portfolio span contributed to which score, whether the recruiter actually reviewed the AI output before deciding.

The shared contract is the **published assessment criteria + `feature_suppression` array** declaring what the agent will and will not consider (race, age, gender, postcode, name-origin proxies, prior-employer status, etc.).

## Regulatory anchors

The author's [ICIS 2026 paper](https://github.com/jhcontext/jhcontext-papers/tree/main/icis) on the Responsibility and Ethics track already maps PAC-AI to the hiring domain across nine regulatory instruments — those are the dove-hire regulatory baseline:

- **EU AI Act** Annex III §4 (employment, workers management, access to self-employment)
- **EU GDPR** Art 22 (right to human review of solely automated decisions)
- **NYC Local Law 144** (annual bias audit + pre-deployment notice for Automated Employment Decision Tools)
- **EEOC** UGESP four-fifths rule + 2023 EEOC guidance on AI selection tools
- **EU Directive 2002/14/EC** information & consultation rights when "substantial changes in work organisation" are introduced
- **CJEU SCHUFA C-634/21** Art 22 GDPR extension to scoring
- **Colorado AI Act** SB 24-205 high-risk-AI consumer protection
- **California CPPA ADMT** regulations (effective 2027-01-01) — pre-use notice + opt-out + access right
- **US state hiring AI laws** (IL AIVIA, MD HB1202)

The dove-hire paper will need to add the candidate-facing provenance-query surface on top of the ICIS architecture, and add jurisdictions the ICIS paper does not yet cover (Brazilian CLT + LGPD employment provisions; UK Equality Act 2010 + UK GDPR; possibly Singapore PDPA + the IMDA AI Verify framework).

## Why later, not now

Three reasons to defer:

1. **Validate the pattern in a fiduciary domain first.** dove-edu's pattern works in a pedagogical relationship; dove-health will prove (or break) it in a fiduciary one. Hiring is fiduciary-with-adversarial-edges — the candidate's interests can be genuinely opposed to the recruiter's. The pattern needs to be road-tested in straight-fiduciary (medicine) before being stretched to fiduciary-adversarial (hiring).

2. **The ICIS paper is the regulatory baseline.** Whatever dove-hire becomes, the ICIS paper is the regulatory reference. The dove-hire paper should *cite* ICIS the way dove-health will cite the AIiH papers — building on, not duplicating.

3. **The Vorrai roadmap absorbs some of the recruiter-side energy.** Vorrai's clinic-receptionist wedge handles a chunk of the "regulated front-desk AI" surface that dove-hire would otherwise compete with. Better to let Vorrai mature on the clinical-receptionist side and dove-hire take the *fairness-audited-selection* surface specifically, with no overlap.

## When

After dove-health v1 ships and the *npj Digital Medicine* paper is accepted (or definitively rejected with reviewer feedback). That puts dove-hire scaffolding work in the **2027** band, with a paper target of **ICIS 2027** or **AAAI / FAccT 2027** depending on what dove-health's reviewer pool tells us about how to position multi-agent compliance work.

## Target venues (provisional)

- **FAccT** (ACM Conference on Fairness, Accountability, and Transparency) — primary candidate for the dual-audience candidate-facing-rights framing
- **ICIS** (International Conference on Information Systems) — Responsibility and Ethics track; would be a natural sibling to the author's existing ICIS hiring paper
- **AIES** (AAAI/ACM Conference on AI, Ethics, and Society) — fallback if neither FAccT nor ICIS lands

## Open questions to revisit after dove-health

1. Does the role-aware refusal contract scale to **adversarial** audience pairs (candidate may have reasons to game the rubric), or does the pattern presume cooperative audiences?
2. How does the patient-facing provenance-query surface (dove-health v2) translate to a candidate-facing one? Candidates ask for evidence under different rights regimes (Art 22 review vs. Art 86 explanation vs. anti-discrimination disparate-impact disclosure), and the answers look different.
3. Is the `feature_suppression` array enough for hiring, or does the architecture need an explicit `verify_disparate_impact` verifier that runs across the *cohort* of recent decisions, not just per-decision?

---

*This document will be re-opened after dove-health v1. Until then, please do not start scaffolding `dove-hire-backend` / `dove-hire-frontend` — the architecture is intentionally undecided.*
