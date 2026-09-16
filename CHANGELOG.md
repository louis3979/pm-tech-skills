# Changelog

All notable changes to this marketplace are documented here. The newest `## vX.Y.Z` heading is the current released version — `marketplace.json` and every plugin's `plugin.json` are kept in lockstep with it (checked by `scripts/validate.py`).

## v3.1.0 — 2026-09-16

### Added
- **`pm-memory`**: `memory-verify-claim` skill + `/verify-claim` command — checks a specific time-sensitive claim (market fact, competitor behavior, industry stat) against live current sources via web search instead of relying on possibly-stale training-data recall, and updates its provenance tag once confirmed. Applies a lesson from `upstash/context7` (fetch live docs instead of hallucinating from stale recall) to PM research claims rather than library/API docs — a plain web-search-driven skill, not a hosted indexing service; no dependency on Context7's own infrastructure.
- Light cross-references (natural-language, no hard dependency) added to `memory-hypothesize`, `pr-faq-writer`, and `product-strategist` suggesting `memory-verify-claim` when a load-bearing claim is tagged `(industry-knowledge)` or `(intuition, PM, <date>)`.

### Fixed (from an end-to-end QA pass)
- `prd-writer`: an unresolved permission no longer gets asserted as a guessed Yes/No in the Permissions table while separately flagged as unresolved in Open Questions — now written as `Open — see Open Questions` consistently.
- `product-prioritizer`: added a dedicated "Unscored: Tech Debt / Infra" output section for backlog items with no natural Reach/Impact, instead of forcing a fake score or dropping them silently.
- `memory-ingest`: now explicitly creates a new `stakeholders/<person>.md` from `_SCHEMA.md` on a person's first mention, instead of leaving undefined what happens when no file exists yet.

## v3.0.0 — 2026-09-12

### Added
- **BMAD-inspired skills**, adapted from `bmad-code-org/BMAD-METHOD` as self-contained skills with no dependency on that project's own scaffold/tooling:
  - `pm-tech-product`: `structured-brainstormer` (named-technique divergent brainstorming), `sprint-retrospective` (lightweight recurring retro), plus `/brainstorm` and `/sprint-retro`.
  - `pm-leadership`: `pr-faq-writer` (Amazon Working Backwards), `advanced-elicitation` (menu-driven critique techniques), `course-correction-planner` (mid-delivery disruption triage), `party-mode-debate` (simulated multi-persona roundtable), plus `/write-prfaq`, `/sharpen`, `/correct-course`, `/party-mode`.
- **Governance/CI**: `scripts/validate.py` (manifest/frontmatter/README-sync validator, zero third-party dependencies), a real `.github/workflows/tests.yml` ("Tests" badge) replacing the placeholder `blank.yml`, `CONTRIBUTING.md`, `SECURITY.md`. README also gained "PRs welcome" and "Tests" badges.

### Changed
- Version numbers across `marketplace.json` and all `plugin.json` files reset to a single consistent `3.0.0` (previously drifted independently — a gap this release's CI now prevents from recurring).

## v2.0.0 — 2026-09-11/12

### Added
- **pm-memory** plugin (10 skills, 10 commands): a markdown-native project memory system — source → ingestion → durable knowledge/hypotheses/decisions/stakeholders layers, plus a weekly maintenance sweep. Inspired by the second-brain model in `phuryn/pm-brain`, rebuilt independently.
- **PMBOK-grounded delivery skills** in `pm-tech-product`: `wbs-scope-decomposer`, `schedule-critical-path-analyzer`, `risk-register-manager`, `change-control-manager`, `project-metrics-tracker`, plus `/plan-delivery-risk`.
- **Requirements-core and strategy skills**, closing gaps identified against a Head-of-Product skill reference: `pm-tech-product` gained `prd-writer`, `requirement-analyzer`, `state-machine-designer`, `acceptance-criteria-generator`, `user-story-writer`, `sprint-planner`, `/write-prd`; `pm-leadership` gained `product-strategist`, `roadmap-planner`, `product-prioritizer`, `/set-strategy`.
- Stakeholder power/interest mapping and project closure/retrospective skills in `pm-leadership`.

### Changed
- `pm-erp-domain` (16 ERP/retail/inventory-vertical skills) removed to keep the marketplace focused on generic technology/IT product work rather than business-vertical domain knowledge; 6 domain-agnostic skills from it (RBAC, approvals, audit trail, data consistency, document numbering, reconciliation) were kept and merged into `pm-tech-product`.

## v1.0.0 — 2026-09-11

### Added
- Initial release: `pm-tech-product` and `pm-leadership` plugins, independently built (not a fork) — see each plugin's README for its skill/command list.
