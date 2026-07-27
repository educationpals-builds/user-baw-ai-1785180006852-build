# "Why does it merge my clauses?" probe kit for any attention setup you're about to trust

## The Specimen

A compound sentence where clause boundaries blur:

```
The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained.
```

Dimension: 5 clauses, 1 sentence, 0 explicit delimiters between causal chains.

## The Verdict

Attention mechanisms in transformer architectures blend adjacent tokens when clause boundaries lack explicit markers. This causes:
- Causal attribution errors (which event caused which?)
- Relationship merging (treating sequential events as simultaneous)
- Agent confusion (who did what?)

**Severity: Medium-High** — Silent corruption of logical relationships.

## The Tripwire

If your attention setup cannot separately identify:
1. The crash event
2. The cache overflow (cause)
3. The log fill (parallel cause)
4. The restart action
5. The user complaints (concurrent event)

...then it is merging your clauses. Do not trust causal reasoning from this setup.

## One-Paste Rebuild Block

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Identify each clause boundary. For each clause, state:
- The agent (who/what acts)
- The action
- The causal relationship to adjacent clauses
- Confidence score (0-100)

FAIL CONDITION: Any clause merged with another, any causal arrow reversed, any agent misattributed.
```

---

**Build**: baw.v3 | **Status**: ai_drafted | **Provenance**: see `.ep/provenance.json`

<!-- educationpals-build-verified -->