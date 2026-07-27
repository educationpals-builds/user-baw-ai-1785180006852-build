# Verification Protocol

This document provides stranger verification: a third party can confirm the probe kit works as specified.

---

## Seeded Specimen

Use this exact string:

```
The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained.
```

---

## Verification Steps

### Step 1: Load the Interrogator

Copy the full interrogator spec from `blueprints/head-map-interrogator.md` into your target chat interface.

### Step 2: Submit the Specimen

Paste the seeded specimen and request full analysis.

### Step 3: Confirm Unowned-Relationship Finding

The tool MUST surface a finding about the "and" connector between "cache overflowed" and "logs filled up". Specifically:

**Required output elements:**
- Identification of the "and" as a relationship marker
- Classification as AMBIGUOUS or explicit uncertainty flag
- Statement that the relationship between these two events is not fully specified by the text

**Failure condition:** If the tool states with high confidence that both events are parallel causes OR sequential events without flagging ambiguity, verification fails.

### Step 4: Confirm Numerical Demand

The tool MUST demand a numerical measurement for the unowned-relationship finding. Acceptable forms:

- "Confidence: [0-100]"
- "Ambiguity score: [number]"
- "Rate your certainty from 0 to 100"
- Binary score demand (0 or 1)

**Failure condition:** If the tool provides only qualitative assessment ("somewhat ambiguous", "possibly unclear") without a number, verification fails.

---

## Verification Checklist

| Check | Pass | Fail |
|-------|------|------|
| Specimen accepted without modification | ☐ | ☐ |
| "and" connector identified | ☐ | ☐ |
| Ambiguity flagged for "and" relationship | ☐ | ☐ |
| Numerical measurement demanded | ☐ | ☐ |
| All five clauses individually reported | ☐ | ☐ |

**Verification status:** PASS requires all five checks marked Pass.

---

## Expected Output Sample

A passing interrogator will produce output resembling:

```
CLAUSE [2]: "the cache overflowed"
AGENT: cache
ACTION: overflowed
RELATIONSHIP TO PRIOR: causal (confidence: 85)
MERGE RISK: low

CLAUSE [3]: "the logs filled up"
AGENT: logs
ACTION: filled up
RELATIONSHIP TO PRIOR: ambiguous (confidence: 45)
MERGE RISK: high — "and" does not specify if parallel cause or sequential event

[...]

Alex, this clause shows ambiguous relationship. The model merges nearby tokens. Apply the fix: split clauses with clear punctuation.

MEASUREMENT: Ambiguity flag score = 1 (uncertainty correctly surfaced)
```

---

## Stranger Verification Attestation

After completing verification, record:

- Date: _______________
- Verifier (optional): _______________
- Target system (no vendor names): _______________
- Result: PASS / FAIL
- Notes: _______________