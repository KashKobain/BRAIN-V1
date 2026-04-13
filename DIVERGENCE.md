# DIVERGENCE.md

## What This Repo Is — and What It Isn't

This repository contains the **cognitive skeleton** of BRAIN: the reasoning model, the 23-skill taxonomy, and the identity layer that activates inside Claude Code.

It is not the full system.

The full system is a private, locally-deployed skill library that this repo's architecture governs. The relationship is precise:

```
MANIFEST.md + CLAUDE.md  →  WHO Claude Code is when it opens a project
~/.claude/skills/ (private)  →  WHAT it can actually do once active
```

One is the constitution. The other is the government.

---

## The Private Layer

The operational skill library (`three-plane-skills-v1`, 655 entries) is organized around a **network engineering metaphor** — the same mental model used to operate production infrastructure at scale:

| Plane | Analog | Function |
|-------|--------|----------|
| `mgmt/` | Management plane | System identity, memory, bootstrap, self-improvement |
| `ctrl/` | Control plane | Agent orchestration, routing, security evaluation |
| `data/` | Data plane | Domain execution — where actual work happens |

This maps cleanly onto the 6-plane cognitive model in `CLAUDE.md`:

| Cognitive plane (public) | Operational plane (private) | Notes |
|--------------------------|-----------------------------|---------|
| Perception | `mgmt/` bootstrap + context-mapping | Environment read on session open |
| Executive | `ctrl/` routing + task-decomposition | Orchestration layer |
| Control | `ctrl/` constraint-enforcement + session-bootstrap | Boundary enforcement |
| Reasoning | `data/` domain skills (pentest-sim, network-lab, forensics) | Where inference runs |
| Awareness | `mgmt/` metacognition + `hyperagent/` novelty scoring | Self-monitoring loop |
| Judgment | `ctrl/` skill-security-review (BLOCK/REVIEW/ALLOW) | Security verdict layer |

---

## Key Components Not in This Repo

### `hyperagent/` — Darwin Gödel Machine
Self-improvement loop. Runs a novelty-weighted tournament selector across skill variants. When a skill underperforms, it generates candidate mutations and selects for fitness. This is the operational implementation of the "Self-Improvement Loop" described in `CLAUDE.md`.

### `skill-security-review` — Security Verdict Layer
Operational version of Skill 23 (`ethical-reasoning`). Emits structured verdicts:
```
{ verdict: BLOCK | REVIEW | ALLOW, tactic: ATT&CK-tag, confidence: float }
```
Every agent action passes through this layer before execution. The `CLAUDE.md` version is the reasoning model; this is the enforcement engine.

### `atomic-kb` — Persistent Knowledge Store
Session memory implementation. Uses `window.storage` schema to persist learned patterns across context resets. Solves the "Apply" step in `CLAUDE.md`'s self-improvement loop — this is where "carry this forward" actually goes.

### Domain Skills (`data/` plane)
- `pentest-sim` — chains PT0-003 exam objectives to MITRE ATT&CK techniques
- `network-lab` — Cisco IOS/CCNA/CCNP operational patterns
- `cross-domain-forensics` — multi-system evidence correlation
- `agent-threat-intel` — MITRE ATT&CK-mapped threat modeling

---

## Why the Split Is Intentional

The cognitive skeleton (this repo) is designed to be:
- **Shareable** — anyone can add MANIFEST.md + CLAUDE.md to Claude Code and get a structured cognitive layer
- **Forkable** — the 6-plane model is a starting point, not a ceiling
- **Auditable** — the reasoning architecture is visible without exposing operational details

The operational library (private) contains:
- Workflow details specific to production environments
- Security evaluation logic that shouldn't be public attack surface
- Domain skills built for specific professional contexts (USAF network operations, pentesting)

Making the full library public would expose workflow details that aren't appropriate to share. Making the reasoning model private would prevent it from being useful. The split is intentional.

---

## For Evaluators

If you're reading this as part of a technical evaluation:

The 23 skills in `CLAUDE.md` are not aspirational. Each one maps to a concrete operational component in the private layer. `ethical-reasoning` → `skill-security-review`. `state-maintenance` → `session-bootstrap` + `atomic-kb`. `metacognition` → `hyperagent/` novelty scoring.

The cognitive taxonomy was derived from the operational system, not the other way around.

The documentation is the proof. The proof is the portfolio. The portfolio is the argument.

---

## Current Status

| Layer | Status |
|-------|--------|
| Cognitive skeleton (this repo) | ✅ Deployed 2026-04-12 |
| 3-plane skill library (private) | ✅ v1 — 655 entries, local Mac install |
| `hyperagent/` self-improvement loop | ✅ Operational |
| `skill-security-review` + ATT&CK mapping | ✅ Operational |
| Public distribution / productization | 🔄 In progress |

---

*Built by Kaylan Jones (KashKobain)
Air Force NCOIC — Network Operations / Cyber Operations
Building AI infrastructure that works in reality, not just in papers.*
