# Split-Walk Prompt Pack

Five standalone prompts for clause-merge interrogation. Each prompt is self-contained and ends with the specific measurement it demands.

---

## Prompt 1: Clause Boundary Detection

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Identify every clause boundary in this sentence. A clause boundary exists where one subject-verb unit ends and another begins.

OUTPUT FORMAT:
- List each boundary as: [word before] | [word after]
- State total boundaries found

MEASUREMENT DEMANDED: Report the integer count of boundaries detected. Expected: 4. Report your count and the delta from expected.
```

---

## Prompt 2: Agent Extraction

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Extract every agent (entity performing an action) from this sentence. An agent is a noun or noun phrase that serves as the subject of a verb.

OUTPUT FORMAT:
- List each agent with its associated action
- Format: AGENT: [name] → ACTION: [verb phrase]

MEASUREMENT DEMANDED: Report the integer count of unique agents. Expected: 5 (server, cache, logs, admin, users). Report your count and list any missing or extra agents.
```

---

## Prompt 3: Causal Chain Mapping

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Map every causal relationship in this sentence. A causal relationship exists when one event is stated or implied to cause another.

OUTPUT FORMAT:
- List each causal link as: [cause event] → [effect event]
- For each link, state the textual evidence (the connector word)
- State confidence (0-100) for each link

MEASUREMENT DEMANDED: Report the integer count of causal links with confidence ≥70. Expected: 3. Report your count, list the links, and flag any links below 70 confidence.
```

---

## Prompt 4: Temporal Relationship Classification

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Identify the temporal relationship marked by "while" in this sentence. Classify it as one of:
- CONCURRENT (events happen at the same time, no causal link)
- CAUSAL (one event causes the other)
- SEQUENTIAL (one event follows the other in time, no causal link)

OUTPUT FORMAT:
- State the two events connected by "while"
- State your classification
- State confidence (0-100)

MEASUREMENT DEMANDED: Report a binary score. If classification is CONCURRENT with confidence ≥70, score = 1. Otherwise, score = 0. Report your score and justify.
```

---

## Prompt 5: Unowned Relationship Detection

```
SPECIMEN: "The server crashed because the cache overflowed and the logs filled up so the admin restarted it while users complained."

TASK: Examine the word "and" connecting "the cache overflowed" and "the logs filled up". Determine if the relationship between these two events is:
- CLEARLY PARALLEL (both independently cause the crash)
- CLEARLY SEQUENTIAL (one happened, then the other)
- AMBIGUOUS (the text does not specify)

OUTPUT FORMAT:
- State your classification
- State the textual evidence for your classification
- State confidence (0-100)
- If AMBIGUOUS, state what additional information would resolve it

MEASUREMENT DEMANDED: Report a binary score. If you classified as AMBIGUOUS or stated confidence <70 for a non-ambiguous classification, score = 1 (correct — you flagged uncertainty). If you classified as non-ambiguous with confidence ≥70, score = 0 (failure — you silently resolved ambiguity). Report your score.
```

---

## Pack Usage

Run all five prompts against your target attention setup. Sum the measurements:

| Split | Max Score | Your Score |
|-------|-----------|------------|
| 1: Boundaries | 4 | ___ |
| 2: Agents | 5 | ___ |
| 3: Causal Links | 3 | ___ |
| 4: Temporal | 1 | ___ |
| 5: Ambiguity | 1 | ___ |
| **TOTAL** | **14** | ___ |

**Trust threshold:** ≥12 for conditional trust, ≥13 for full trust, <12 reject or apply fix.