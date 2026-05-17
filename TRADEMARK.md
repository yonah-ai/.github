# Dove — trademark policy

This is the **trademark policy** for the Dove project. It is separate from the [code licence](LICENSE) (Apache-2.0) because Apache-2.0 explicitly does not grant trademark rights (§6 of the licence). The Dove name, the Dove logo, and any product names of the form `dove-*` (e.g. `dove-edu`, `dove-health`, `dove-hire`) are project trademarks of João Henrique da Rosa.

The policy below is modelled on widely-used open-source trademark policies (Kubernetes, Rust, Linux Foundation) and is deliberately permissive for community use while reserving the brand-identity surface that distinguishes the official project from forks.

## What you may do without asking

- **Fork the code** under Apache-2.0 and modify it however you like. The licence permits this.
- **Refer to the project by name** in documentation, blog posts, tutorials, conference talks, academic papers, comparative reviews, news articles, classroom material, and similar — including using the Dove logo in such references when the use is factual and non-confusing ("I used Dove to evaluate student work").
- **Distribute unmodified releases** of `dove-edu-backend`, `dove-edu-frontend`, or any sibling repo under their official names. The release name is part of the project identity and propagates with the unmodified artefact.
- **Run your own deployment** of an unmodified Dove for your institution, classroom, clinic, or company. Internal use does not constitute a redistribution under the trademark.

## What requires a different name

If you fork the code and **modify it substantially**, please ship your fork under a **different name**. "Dove" identifies a particular project with a particular architectural commitment (dual-audience role separation + signed envelopes + structural verifiers); a modified fork should communicate that it is *not* that project. Common patterns:

- **Add a clear distinguishing prefix or suffix**: "FooDove", "Dove-Compatible", "MyOrg-Dove-Fork". The phrase "based on Dove" or "Dove-derived" is welcome and unambiguous.
- **Replace the name entirely** when the fork has its own identity (this is the Rust ↔ Cargo / Linux ↔ Android pattern).

You do not need our permission to do either of these.

## What requires our permission

- **Selling a product or service under the name "Dove"** or a confusingly similar name (e.g. "Dove AI", "Dove Agent", "Dove Cloud") — especially in the regulated domains we operate in (education, healthcare, hiring).
- **Registering a trademark** that includes "Dove" or a confusingly similar mark in any class touching software, AI, education, healthcare, hiring, or related fields.
- **Using the Dove logo** to brand a commercial product, paid service, or paid event.
- **Implying endorsement** by the Dove project of a third-party product, organisation, or position.

If you want to do any of the above, open a discussion in the [dove-agent/.github](https://github.com/dove-agent/.github) repository describing what you want to do. We are open to community partnerships, especially in the regulated-AI space — we just want them to be deliberate.

## Why the policy exists

Two reasons.

**For the community.** A consistent name + logo lets people who depend on Dove (researchers citing the IJAIED paper, deployers running it in their classrooms or clinics, contributors filing issues) find the *one* official project. If anyone could ship modified versions under the same name, the brand would stop communicating *which* implementation a given user is talking about, and the value of having a published architectural commitment (the personality contract, the refusal policy, the structural verifiers) would erode.

**For trademark hygiene.** The names "Dove" and `dove-*` overlap nominally with the well-known Unilever Dove mark in Class 3 (cosmetics) and Mars's Dove mark in Class 30 (chocolate). Neither is in software, so the open-source software-class use is defensible — but the defence is stronger if (a) there is one project that uses the name and (b) that project has a published trademark policy that *narrows* the scope of permitted use. A loose, undocumented use of the name across many forks would weaken both points.

## Questions

Open a discussion in the [dove-agent/.github](https://github.com/dove-agent/.github) repo and tag it `trademark`. We aim to answer within a week.

## Updates

This policy may evolve. Material changes will be announced in the [dove-agent/.github](https://github.com/dove-agent/.github) repository discussions and noted at the bottom of this file with a date.

**Policy version: v0.1.0 — 2026-05-17.**
