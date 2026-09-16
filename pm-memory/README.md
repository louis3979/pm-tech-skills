# pm-memory

A markdown-native project memory system for a product operator: durable knowledge, decisions, hypotheses, and stakeholder tracking that survives context loss between sessions, with a source-to-knowledge ingestion pipeline, live claim verification, and a weekly maintenance sweep. Inspired by the second-brain model in [phuryn/pm-brain](https://github.com/phuryn/pm-brain), rebuilt in this marketplace's own skill/command conventions — not a copy of its files.

## Overview

One operator, one product/initiative. `/init-memory` scaffolds a folder structure in your project: raw artifacts land in `source/` (immutable), get synthesized into `ingestion/` (tagged observation/interpretation/hypothesis/assumption), and propagate into the durable layer — `knowledge/`, `hypotheses/` (evidence + confidence score), `decisions/` (audit trail + reversal condition), `stakeholders/` (per-person touchpoints and cadence). A weekly `/review` sweep is what keeps it from rotting.

## Install

Add the marketplace and install this plugin (or the whole collection) the same way as any other `pm-skills` plugin — see the root [README.md](../README.md) for the marketplace add/install commands.

## Skills (11)

- **memory-init** — Scaffold the memory folder structure into the current directory; detects greenfield/migration/active-repo, runs a short interview, commits locally (never pushes).
- **memory-ingest** — The workhorse: classify a raw artifact, copy it to `source/`, tag observations in `ingestion/`, propagate to knowledge/hypotheses/stakeholders/decisions as warranted.
- **memory-prep** — Read-only pre-meeting brief for a stakeholder or topic: last touchpoint, open asks, suggested questions.
- **memory-review** — Weekly maintenance sweep: stale knowledge, stale evidence, hypothesis hygiene, stakeholder cadence, knowledge compression, archival.
- **memory-decide** — Formalize a decision with a full evidence trail and reversal condition, drafted `pending` until the operator confirms it.
- **memory-hypothesize** — Draft or update a tracked belief with evidence, confidence score, and a decision trigger.
- **memory-risk-scan** — Five-area risk scan for a feature/initiative, drafting hypothesis stubs for uncovered areas.
- **memory-ideate** — Grounded solution directions for a problem area, tagged with the evidence behind each.
- **memory-plan** — Six-block plan for an objective: known, assumed, who to talk to, hypotheses to open, experiments, decision points.
- **memory-strategy-check** — Check a proposal against stated strategy, citing the specific clause.
- **memory-verify-claim** — Check a specific time-sensitive claim (market fact, competitor behavior, industry stat) against live current sources instead of relying on training-data recall.

## Commands (11)

- `/pm-memory:init-memory` — Initialize the project memory system in the current directory.
- `/pm-memory:ingest` — Ingest a raw artifact into project memory.
- `/pm-memory:prep` — Pre-meeting/pre-task brief for a stakeholder or topic.
- `/pm-memory:review` — Run the weekly maintenance sweep.
- `/pm-memory:decide` — Formalize a decision with an evidence trail.
- `/pm-memory:hypothesize` — Draft or update a tracked hypothesis.
- `/pm-memory:risk-scan` — Five-area risk scan for a feature/initiative.
- `/pm-memory:ideate` — Grounded solution directions for a problem area.
- `/pm-memory:plan` — Six-block plan for an objective.
- `/pm-memory:strategy-check` — Check a proposal against stated strategy.
- `/pm-memory:verify-claim` — Check a specific time-sensitive claim against live current sources.

## What this deliberately doesn't include

Unlike the reference project, this plugin does not ship a `PostToolUse` hook that enforces schema on every file write — that's real infrastructure risk to take on sight-unseen in someone else's project, and the core value (the ingest → durable-layer discipline, the epistemic honesty rules) doesn't depend on it. `memory-review`'s sweep catches structural drift after the fact instead of blocking it in real time. Revisit if this proves insufficient in practice.

`memory-verify-claim` applies a lesson from [upstash/context7](https://github.com/upstash/context7) (don't answer time-sensitive questions from possibly-stale training-data recall — fetch a live, current source and cite it) to PM research claims rather than library/API docs. It's a plain web-search-driven skill, not a hosted documentation-indexing service like Context7 itself — no external API/infrastructure dependency.

## Author

Louis

## License

MIT
