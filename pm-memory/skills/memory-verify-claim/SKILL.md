---
name: memory-verify-claim
description: "Check a specific time-sensitive claim (market fact, competitor behavior, industry stat, technical/regulatory best practice) against live current sources via web search instead of relying on training-data recall, before it's used as evidence. Use before a claim tagged (industry-knowledge) or (intuition, PM, date) gets cited in a PRD, hypothesis, decision, or PR/FAQ, or whenever a claim's currency is actually load-bearing."
---

# Memory Verify Claim

## Purpose

You are checking whether $ARGUMENTS — a specific, time-sensitive claim someone is about to rely on — is actually current, instead of answering from possibly stale training-data recall. The failure mode this exists to catch: a confidently-stated "fact" about a competitor's pricing, a market trend, a compliance requirement, or a technical best practice that was true at training time but has since changed, silently becoming load-bearing evidence in a decision.

## Context

Run this before a claim tagged `(industry-knowledge)` or `(intuition, PM, <date>)` in `memory-hypothesize`/`memory-ingest`/`memory-decide` gets used as real evidence for something consequential — or any time a skill in this marketplace (`product-strategist`, `pr-faq-writer`, `course-correction-planner`, `security-product-reviewer`, and others) states something as fact that is actually time-sensitive and checkable. Not every claim needs this — a claim that isn't actually time-sensitive (a stable definition, an internal fact already in `knowledge/`) doesn't need verification, only ones where being stale would materially change the conclusion.

## Instructions

1. **Isolate the specific, checkable claim** — not the whole surrounding argument. "Competitor X charges $49/seat" is checkable; "Competitor X is aggressive on pricing" is an interpretation, not a fact to verify (though it may rest on checkable facts worth pulling out first).
2. **Search for a live, current source** — don't answer from recall. Look for the primary source where possible (the competitor's own pricing page, the actual regulation text, the vendor's own changelog) over a secondary summary.
3. **Compare against what was assumed**: confirmed as stated, confirmed but outdated (state what changed and when, if datable), contradicted, or genuinely unverifiable (no reliable current source found).
4. **Never fabricate a source or a plausible-sounding URL/date to fill the gap** — if nothing reliable turns up, say so plainly; "unverifiable as of [today's date], proceeding on the original tag" is a legitimate outcome, not a failure.
5. **Update the provenance** wherever this claim is used: if it was tagged `(industry-knowledge)` or `(intuition, PM, <date>)` and is now confirmed with a real source, replace the tag with the actual link and the check date. If it turned out wrong, correct the claim where it's used and note why (don't leave a disproven claim standing).
6. **Flag downstream impact**: if this claim was load-bearing for a hypothesis's confidence score, a decision's rationale, or a PRD's Problem Statement, name what needs re-checking as a result — a corrected fact doesn't automatically fix the conclusion built on it.

## Output

```markdown
## Claim Verification: [claim, stated plainly]

**Original tag**: [e.g. (industry-knowledge) or (intuition, PM, 2026-08-01)]
**Checked**: [date]

**Finding**: Confirmed / Confirmed but outdated / Contradicted / Unverifiable
**Source**: [live source + date, or "none found" if unverifiable]

**Detail**: [what the source actually says, especially if it changed what was assumed]

**Downstream impact**: [what else — a hypothesis, decision, PRD section — relied on the old version of this claim and should be revisited; or "none" if this was checked before being used anywhere]
```

If project memory (`pm-memory`) is in use, apply the update directly to wherever the claim's provenance tag lives (a `hypotheses/` evidence row, a `decisions/` evidence trail, `knowledge/market.md`); otherwise return the finding inline for the caller to use.

## Notes

- "Unverifiable" is a real, useful answer — don't strain to manufacture a source, and don't silently fall back to stating the original claim as if it were confirmed.
- A claim that was true 18 months ago stated with total confidence today is exactly the failure mode this skill exists to catch — treat "when was this last actually checked" as a real question, not a formality.
- This is about specific, checkable facts — not a substitute for `problem-validator` (which validates whether a user problem is real) or `memory-ingest` (which processes a whole raw artifact, not one isolated claim).

## Example

Input: "Our PR/FAQ's Internal FAQ says 'Competitor Y doesn't offer an API, so this is a clear differentiator' — tagged (industry-knowledge)." Check finds Competitor Y shipped a public API 4 months ago (their own docs site, dated). Finding: Contradicted. Downstream impact: the PR/FAQ's stated differentiator no longer holds — flagged for the PR/FAQ to be revised before it's used to justify the concept, not after.
