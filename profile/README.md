<div align="center">

# Yonah AI

*An academic open-source family of autonomous AI agents with verifiable per-decision provenance.*

</div>

---

*Companion paper at ACM TAAS (in submission, Q4 2026).*

## Repositories

### Framework (vertical-agnostic upstream)

- [yonah-agent](https://github.com/yonah-ai/yonah-agent) — framework backend: Chalice REST + WebSocket API, CrewAI worker, seven-tool surface, three-crew structure, PAC-AI substrate (Apache-2.0)
- [yonah-page](https://github.com/yonah-ai/yonah-page) — framework frontend: React + Vite, pipeline visualisation, role-gated WSS client (Apache-2.0)

### Verticals (forks of the framework)

- **yonah-edu** — education vertical (accompanying paper at IJAIED 2026)
  - [yonah-edu-agent](https://github.com/yonah-ai/yonah-edu-agent) — education backend (Apache-2.0)
  - [yonah-edu-page](https://github.com/yonah-ai/yonah-edu-page) — education frontend (Apache-2.0)
- **yonah-health** — health vertical (paper forthcoming) — *placeholder*
- **yonah-hire** — hiring vertical (paper forthcoming) — *placeholder*

Verticals fork the framework upstream and override the vertical-specific
tool implementations, crew specialisations, and regulatory mapping tables.
Framework improvements are pulled into each vertical via `git pull upstream main`.

## About the name

**Yonah** (יוֹנָה) is the Hebrew word for *dove*. It is also the proper name of the prophet — *Jonah* in English, *Jonas* in Portuguese — whose narrative is, at its heart, a story about reluctant testimony delivered anyway. *Yonah* the bird and *Yonah* the prophet are the same word in Hebrew.

The project name is in tribute to the Holy Spirit, who in the Christian tradition descends and remains as a dove, and to the prophet who shares that name and that mission: to carry a faithful witness to whoever needs to receive it.

> *"When the dove returned to him in the evening, there in its beak was a freshly plucked olive leaf."*
> — Genesis 8:11

The dove returns from over the receding waters carrying evidence that the world has changed. An autonomous AI agent in a regulated domain has, modestly, the same office: to return with verifiable evidence of what was decided, on whose authority, against which artefacts. The agent does not pronounce; it carries the witness.

## Project posture

Yonah AI is **academic open-source work**, accompanying peer-reviewed papers in the author's research portfolio. It has **no commercial purpose**.

---

<div align="center">

*Maintained by [João Henrique da Rosa](https://github.com/jhcontext).*

</div>
