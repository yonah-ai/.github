# dove-agent

GitHub-organisation `.github` repo for **Dove** — a family of dual-audience autonomous AI agents with verifiable per-decision provenance, each scoped to a regulated domain.

Three sister repositories, sharing a common architectural substrate ([jhcontext-sdk](https://pypi.org/project/jhcontext-sdk/) + [jhcontext-protocol](https://pypi.org/project/jhcontext-protocol/) on PyPI), one per vertical:

- **[dove-edu-backend](https://github.com/dove-agent/dove-edu-backend)** + **[dove-edu-frontend](https://github.com/dove-agent/dove-edu-frontend)** — education (professors + students; EU AI Act Annex III §3)
- **dove-health-backend** + **dove-health-frontend** — healthcare (clinicians + supervised second readers, with patient-facing v2; EU AI Act Annex III §5 + MDR Rule 11 + GDPR Art 9). *Roadmap; see [proposals/dove-health.md](proposals/dove-health.md).*
- **dove-hire-backend** + **dove-hire-frontend** — hiring (recruiters + candidates; EU AI Act Annex III §4 + GDPR Art 22 + NYC LL144 / EEOC / Colorado AI Act). *Roadmap; see [proposals/dove-hire.md](proposals/dove-hire.md).*

This repo (the org-level `.github` repo) carries the things that are shared across all three Doves: the **org profile page** rendered at github.com/dove-agent, the **logo prompt and brand spec**, and the **per-vertical proposals** that pin each sister repo to a target academic venue.

## Layout

```
dove-agent/                       (this repo, name `.github` in the org)
  profile/README.md               rendered as the github.com/dove-agent landing page
  brand/
    logo_prompt.md                the canonical Dove logo image-generation prompt
    colors.md                     palette + typography spec (adapted from vorrai)
  proposals/
    dove-health.md                v1 architecture sketch + target venue
    dove-hire.md                  placeholder; design after dove-health is published
  LICENSE                         Apache-2.0
  README.md                       this file
```

## License

Apache-2.0. Brand assets (rendered logos, illustrations) released under CC BY 4.0 from the dove-edu / dove-health / dove-hire brand folders, not here.
