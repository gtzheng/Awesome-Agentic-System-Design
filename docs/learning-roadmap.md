# Learning roadmap

[Home](../README.md) · [Architecture](architecture.md) · [Interview preparation](interview-preparation.md)

The topics below form a path from agent fundamentals to production systems. Basic programming, HTTP APIs, databases, and familiarity with LLM prompts and tokens provide useful background.

## Topic sequence

| Topic | Resources | Key concepts |
| --- | --- | --- |
| 1. The agent loop | [Architecture](architecture.md); [ReAct](https://arxiv.org/abs/2210.03629) | Actions, observations, control flow, run state, and termination |
| 2. Grounding and tools | [Context and memory](context-and-memory.md); [tool contracts](tools-and-protocols.md) | Retrieval, citations, context selection, schemas, and authorization |
| 3. Quality and recovery | [Evaluation](evaluation.md); [production](production-and-safety.md) | Success criteria, traces, durable execution, fault recovery, and side effects |
| 4. Design tradeoffs | [Case studies](case-studies.md); [interview guide](interview-preparation.md) | Architecture choices, quality, cost, latency, and failure behavior |

## Paths by focus

| Focus | Path | Coverage |
| --- | --- | --- |
| Fundamentals | [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) → [architecture](architecture.md) → [context and memory](context-and-memory.md) | Workflow patterns, tool loops, and information management |
| Production systems | [Tools and protocols](tools-and-protocols.md) → [production and safety](production-and-safety.md) → [evaluation](evaluation.md) | Execution contracts, operational failures, and quality measurement |
| Interview preparation | [Interview guide](interview-preparation.md) → [case studies](case-studies.md) | Design questions, quantitative examples, and worked architectures |
| Research | [Paper catalog](../resources/papers.md) → [recent developments](../UPDATES.md) | Research organized by design question, with dated developments |

## Illustrative comparisons

| Comparison or scenario | Design question |
| --- | --- |
| Fixed workflow and model-selected actions | Which decisions depend on intermediate observations? |
| Full history, structured summaries, and retrieved evidence | How do context choices affect retained constraints and token use? |
| A timeout after an external write commits | How can a resumed run establish the outcome and avoid a duplicate action? |
| A retrieved document containing malicious instructions | Which controls prevent the content from gaining execution authority? |
| One research agent and parallel workers with equal budgets | How do coverage, coordination overhead, and total cost differ? |
| A changed model or prompt on the same held-out cases | Which task categories improve or regress? |

## Key terms

| Term | Meaning in this repository |
| --- | --- |
| Harness / runtime | Software managing the model loop, tools, context, state, permissions, and execution |
| Trajectory | The observable sequence of messages, actions, results, and state transitions in a run |
| Context | Information provided to a model for a particular invocation |
| Memory | Information deliberately persisted for later retrieval or reuse |
| Checkpoint | Persisted execution state sufficient to resume under defined recovery semantics |
| Handoff | Transfer of responsibility or control to another agent or a human |
| Grounding | Supporting output with relevant evidence from an identified source |
| Evaluation | Measuring behavior against an explicit task, environment, and success criterion |
| Guardrail | A validation or detection mechanism; its guarantees depend on its enforcement |
| Idempotency | Repeating the same logical operation does not create an additional effect |

## Resource types

[Guides](../resources/guides.md) cover practical explanations and specifications. [Papers](../resources/papers.md) examine research questions and approaches. The [framework catalog](../resources/frameworks.md) describes implementation tools and their design considerations. [Updates](../UPDATES.md) records releases, migration notes, and recent research.
