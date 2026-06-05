---
title: the prototype is the spec
date: 2026-04-01
room: workshop
tags: [tech, product]
excerpt: "we've been running a trial on my team — making all the pms learn git and contribute to code. not because i want them to become developers. because the old workflow is too slow for 2026."
draft: false
---

not because i want them to become developers. because i think the old workflow — write a spec, hand it to design, hand it to dev, watch it get built differently than you imagined — is genuinely too slow for 2026. and there's a better way now.

it wasn't a grand plan. i set up a demo project with one of our frontend devs for an internal event. react + vite, nothing fancy. we used it to show a workflow to stakeholders, it went well, and then we just... kept going. that demo project is now the base we're building everything on. that's usually how the good stuff starts. not a roadmap item, just a thing that worked.

the idea is simple. pms build working prototypes — using claude, codex, whatever — and check them with stakeholders before anything goes to development. not wireframes, not figma screens. something you can actually click through.

while stakeholders are reviewing the UI, we wire up a service layer in parallel. the backend team looks at the live prototype and figures out what data needs to be sent, what needs to stay as frontend logic, what the endpoints should look like. they're not reasoning from a requirements doc. they're looking at a real thing.

by the time stakeholders sign off on the UI, the backend team isn't starting from zero. the API contract is already being shaped. the handover is an actual artifact — commits, a codebase, a working demo — not a conversation.

most teams skip the git part and end up with a graveyard of figma files and dead demo links. nobody can trace what version was shown to who. decisions get lost. git at the level a pm needs it — clone, branch, commit, push, raise a pr — is maybe a day of discomfort and then it's muscle memory. the "it's too technical" excuse has a pretty short shelf life when the tools are this accessible.

something shifts once a pm has shipped even one prototype that went from their laptop to a stakeholder demo. they stop thinking of themselves as the person who writes specs. that mindset change is worth more than any individual skill.

this isn't a moonshot. it's just contract-driven development with a shorter feedback loop. the data shapes, the actions, the states the UI needs to handle — all of it is already implicit in a working prototype. formalising it into a service layer isn't extra work, it's the natural next step.

we're still building this out. but so far: it works.
