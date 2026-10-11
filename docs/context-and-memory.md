# Context, retrieval, and memory

[Home](../README.md) · [Architecture](architecture.md) · [Tools and protocols](tools-and-protocols.md)

Context is information available for one model call. Memory is stored information selected for later use. Execution state records what the system has actually done. These have different correctness and retention requirements.

## Separate information by purpose

| Information | Example | Storage / access | Correctness concern |
| --- | --- | --- | --- |
| Task context | Request, constraints, evidence | Assembled per invocation | Constraints survive truncation |
| Execution state | Approval, completed tool call | Durable transactional store | Recovery does not repeat an action |
| Knowledge | Product policy, repository files | Search/index plus source of truth | Freshness, access control, citations |
| Episodic memory | Previous interaction outcome | Scoped, timestamped records | An earlier error is not promoted to fact |
| User preferences | Language or report format | User-editable profile | Consent, correction, deletion |
| Procedural knowledge | Reusable task procedure | Versioned instructions or skills | Trusted origin and compatible tools |

## Build a context budget

Reserve space for tool results and model output. Prioritize active constraints, recent observations, and evidence needed for the next decision. Keep large artifacts outside the prompt and retrieve relevant sections using stable identifiers.

```text
available input ≈ context limit − reserved output − system/tool overhead − margin
```

Measure relevant evidence per token, repeated content, and constraints lost after compaction. A larger window changes capacity; it does not establish that all information will be used correctly. [Effective context engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) discusses selective retrieval, compaction, notes, and separate agent contexts.

## Start with ordinary retrieval

A baseline is: authenticate → retrieve authorized sources → rank evidence → generate with citations → check support. Use keyword search for exact identifiers, semantic search for paraphrased concepts, and structured queries for data with a schema. Combine methods when measured failures justify it.

Agentic retrieval adds decisions such as rewriting a query, selecting another source, or continuing a search. Search limits and criteria for sufficient evidence determine when retrieval stops. See the [Agentic RAG survey](https://arxiv.org/abs/2501.09136) for a research map.

Evaluate retrieval and generation separately. If the correct policy never reached the model, changing the answer prompt may hide the real problem.

## Compact without losing the task

Use a structured continuation record:

```text
Goal and user constraints
Completed steps with receipt or artifact references
Current hypotheses, marked as unverified
Evidence references and source timestamps
Pending operations and approvals
Next step, remaining budget, and stopping conditions
```

Retain source records for verification. Do not replace the action ledger with a model-written narrative. Test resumption after compaction with contradictory evidence and a pending write.

## Design memory writes as a product feature

Decide what qualifies for persistence, who owns it, how it expires, and how users correct it. Include subject, scope, source, timestamp, expiry, and whether a record is a user statement, verified fact, or inference.

Retrieve within the authenticated tenant and user scope. Apply those boundaries to indexes, caches, summaries, and traces. Invalidate derived records when permissions or sources change. Deleting an original while retaining a revealing summary is incomplete deletion.

Treat memories as data. They must not override permissions or trusted instructions. [A-MEM](https://arxiv.org/abs/2502.12110) explores structured, linked memory. Compare its retrieval quality and maintenance cost with your baseline.

## Questions to test

- Can the agent identify an outdated policy and retrieve the current one?
- Does a correction supersede an older inferred preference?
- Can one tenant's document appear in another tenant's cache or summary?
- After compaction, does the agent retain the user's spending constraint?
- Does extra retrieved content improve answers or introduce conflicting instructions?

**Design question:** how does persistent user memory affect outcomes compared with retrieval alone, and what evidence demonstrates the difference?
