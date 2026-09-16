---
description: Check a specific time-sensitive claim against live current sources instead of relying on training-data recall
argument-hint: "<the claim to verify, e.g. 'Competitor X charges $49/seat'>"
---

# /verify-claim -- Live Claim Verification

Check whether a specific, time-sensitive claim is actually current before it gets relied on as evidence — instead of answering from possibly-stale recall.

## Invocation

```
/verify-claim Competitor X doesn't offer a public API
/verify-claim GDPR requires explicit opt-in for this kind of data use
/verify-claim [any specific, checkable, time-sensitive claim]
```

## Workflow

### Step 1: Isolate the Claim

Confirm the specific, checkable fact — not the broader argument around it. If what's given is really an interpretation ("they're aggressive on pricing"), ask for or extract the underlying checkable fact first.

### Step 2: Verify

Apply the **memory-verify-claim** skill: search for a live, current, ideally primary source; compare against what was assumed; render a Confirmed / Confirmed but outdated / Contradicted / Unverifiable finding — never fabricate a source.

### Step 3: Propagate

If project memory is in use and this claim already lives somewhere (a hypothesis's evidence row, a decision's evidence trail, `knowledge/market.md`), update its provenance tag and flag anything downstream that was built on the old version.

### Step 4: Offer Next Steps

- "Want me to **update the hypothesis/decision** this claim was feeding (`memory-hypothesize` / `memory-decide`)?"
- "Should I **check for other claims in the same document** that might also be stale?"

## Notes

- "Unverifiable, no reliable current source found" is a legitimate, useful result — don't accept a manufactured-sounding source instead.
- Not every claim needs this — only ones where staleness would actually change a conclusion someone is relying on.
