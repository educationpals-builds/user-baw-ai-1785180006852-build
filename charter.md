# Clause-Merge Interrogation Charter

## Specimen Definition

**Input string:**
```
The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained.
```

**Dimension arithmetic:**
- Token count (approx): 19
- Clause count: 5
- Explicit delimiters: 0 (no semicolons, no periods mid-sentence)
- Causal connectors: 3 ("because", "so", "while")
- Coordinating conjunctions: 1 ("and")
- Ambiguity surface: High ("and" could be causal or temporal)

## Standard

A trustworthy attention setup MUST:
1. Preserve clause individuality under tokenization
2. Correctly attribute causal direction
3. Distinguish temporal concurrence ("while") from causal sequence ("so")
4. Not hallucinate relationships absent from the text
5. Report uncertainty when boundaries are ambiguous

## Five Split Findings

### Split 1: Clause Boundary Detection
**Finding:** Boundaries at positions [crashed|because], [overflowed|and], [filled up|so], [restarted it|while]
**Measurement:** 4 boundaries detected / 4 expected = 100% or failure count

### Split 2: Agent Extraction
**Finding:** Agents are {server, cache, logs, admin, users}
**Measurement:** 5 agents / 5 expected

### Split 3: Causal Chain Mapping
**Finding:** cache overflow → crash; log fill → crash (parallel cause); crash → restart
**Measurement:** 3 causal links correctly directed

### Split 4: Temporal Relationship
**Finding:** "users complained" is concurrent with "admin restarted", not caused by it
**Measurement:** Binary — concurrent correctly identified (1) or merged as causal (0)

### Split 5: Unowned Relationship Detection
**Finding:** The "and" between overflow and fill-up has ambiguous ownership — could be parallel causes or sequential events
**Measurement:** Ambiguity flagged (1) or silently resolved (0 — failure)

## Severity Story

When clause merging occurs silently:
- Legal documents lose liability boundaries
- Medical notes confuse symptom sequences
- Incident reports misattribute root causes
- User intent in compound queries gets flattened

**Severity gradient:** Low (cosmetic) → Medium (confusion) → High (wrong causal model) → Critical (action on false causation)

This specimen sits at **High** — it will produce wrong causal models if merged.

## Call

Before trusting any attention setup with compound reasoning:
1. Run this specimen
2. Demand numerical scores for each split
3. Reject any setup that scores below 80% on splits 1-3 or fails split 5

## Tripwire

**Automatic distrust trigger:**

If the setup returns "the cache overflow and logs filling caused the crash" as a single merged cause without distinguishing the two events, the tripwire fires. This indicates token-proximity merging is active.

## Builder's Run

1. Load specimen into target system
2. Execute prompts from `prompts/split-walk-pack.md` in sequence
3. Record numerical output for each split
4. Compare against standard
5. Document in `VERIFY.md` format
6. Decide: trust, conditional trust with fix, or reject