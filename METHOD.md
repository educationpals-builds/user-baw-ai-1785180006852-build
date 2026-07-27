# METHOD: The PRISM Framework for Clause-Merge Interrogation

This document defines the five principles for auditing attention-based systems against clause merging. The acronym PRISM encodes the methodology.

---

## P — Partition

**Principle:** Divide the specimen into atomic units before analysis.

A compound sentence is not one thing. It is multiple clauses wearing a single period. Partition first, always.

**Practice:**
- Identify clause boundaries by subject-verb pairs
- Mark connectors (because, and, so, while) as boundary signals
- Never analyze a compound structure as a monolith

---

## R — Run in Parallel

**Principle:** Test each clause independently and simultaneously.

Sequential analysis allows earlier findings to contaminate later ones. Parallel runs isolate each clause's behavior.

**Practice:**
- Submit each clause as a separate query
- Compare outputs for consistency
- Detect when the system "remembers" across clauses (leakage)

---

## I — Individuate

**Principle:** Each clause must retain its own agent, action, and relationships.

Merging occurs when individuation fails — when two agents become one, when two actions blur, when relationships lose their owners.

**Practice:**
- Demand explicit agent extraction per clause
- Require relationship attribution (which clause connects to which)
- Flag any output that combines distinct entities

---

## S — Stitch

**Principle:** Reconstruct the whole only after validating the parts.

Stitching is the controlled inverse of partitioning. You rebuild the compound structure, but now with verified boundaries.

**Practice:**
- Reassemble clauses with explicit delimiters
- Verify that stitched output matches partitioned findings
- If mismatch: the system merged during reconstruction

---

## M — Map

**Principle:** Produce a visual or structured representation of all relationships.

The map is the artifact. It shows causal chains, temporal overlaps, and ambiguity zones. Without a map, you have no proof of correct parsing.

**Practice:**
- Generate clause-relationship diagrams
- Mark confidence levels on each edge
- Highlight unowned or ambiguous relationships

---

## The Collapse Anti-Pattern

**Definition:** Collapse occurs when the system skips PRISM and processes the compound sentence as a single semantic unit.

**Symptoms:**
- Agents merged ("the system" instead of "server, cache, logs, admin, users")
- Causal chains flattened ("everything caused the crash")
- Temporal relationships lost ("while" treated as "and")
- Ambiguity silently resolved (no uncertainty flagged)

**Cause:** Attention mechanisms weight nearby tokens together. Without explicit delimiters, clause boundaries become invisible to the model.

**Consequence:** The model outputs confident, coherent, wrong causal models.

**Detection:** Run the five splits from `prompts/split-walk-pack.md`. Any score below threshold indicates collapse.

**Remedy:** Apply the fix — split clauses with clear punctuation before submission.

---

## PRISM Summary

| Letter | Principle | Anti-Pattern Blocked |
|--------|-----------|---------------------|
| P | Partition | Monolith processing |
| R | Run in parallel | Sequential contamination |
| I | Individuate | Agent/action merging |
| S | Stitch | Reconstruction drift |
| M | Map | Invisible relationships |

Apply PRISM to any attention setup before trusting it with compound reasoning.