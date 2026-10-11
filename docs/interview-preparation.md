# Agentic system design interview guide

[Home](../README.md) · [Learning roadmap](learning-roadmap.md) · [Worked cases](case-studies.md)

This guide covers the requirements, mechanisms, and tradeoffs involved in explaining an agentic system design. Discussion topics, quantitative examples, worked cases, and a self-assessment rubric connect architectural choices with their operational consequences.

## Discussion structure

| Area | Topics |
| --- | --- |
| Requirements | Users, task, permitted actions, success, ambiguity, and human involvement |
| Assumptions | Traffic, latency, cost, data freshness, tenancy, and failure consequences |
| Architecture | API, run queue, runtime, model, tools, retrieval, state, and verification |
| Mechanisms | Retrieval, planning, delegation, and action execution |
| Failure handling | Crash recovery, duplicate effects, injection, unavailable dependencies, and budgets |
| Evaluation and deployment | Test set, graders, metrics, limited rollout, and rollback |
| Tradeoffs | Baselines, alternatives, bottlenecks, and evidence supporting each choice |

## Requirements and assumptions

Requirements describe what the agent must accomplish, its authority to write to external systems, and the evidence that establishes success. Response-time needs determine which work is synchronous and which can run as a background job. The cost of a wrong action, delay, or escalation shapes the control flow.

Explicit assumptions support quantitative reasoning when measurements are unavailable. Product goals and measured behavior provide different inputs to the design.

## Quantitative reasoning

Illustrative assumptions: **100,000 tasks/day**, **10× peak traffic**, **six model calls/task**, **two seconds/model call**, and **three tool calls at 300 ms each**.

- Average task arrival rate: `100,000 / 86,400 ≈ 1.16 tasks/s`.
- Peak arrival rate: `≈ 11.6 tasks/s`; peak model request rate: `≈ 69.4 calls/s`, before retries.
- Serial service time: `6 × 2 + 3 × 0.3 = 12.9 seconds`, before queueing and overhead.
- At that assumed peak rate and mean service time, Little's Law suggests roughly `11.6 × 12.9 ≈ 150` active tasks in steady state. Add headroom and model the latency distribution to estimate p95 latency.
- If a run costs an assumed `$0.02`, gross daily run cost is `$2,000`. At an 80% acceptance rate, cost per accepted task is `$0.025`, excluding human review and other operating costs.

Token throughput and request limits both affect capacity. Parallelism can reduce critical-path latency while increasing total cost. Human approval may dominate elapsed time even when model calls are fast.

## Tradeoff questions and strong answer signals

| Question | What a strong answer covers |
| --- | --- |
| Why an agent instead of a workflow? | A concrete decision that depends on observations; a simpler baseline |
| Why multiple agents? | Independent work or context separation; coordination cost; comparison under equal budgets |
| Why retrieval instead of putting everything in context? | Permissions, freshness, relevance, latency, and evidence preservation |
| Do we need persistent memory? | A specific benefit; write policy, provenance, correction, expiry, and deletion |
| What happens after a tool timeout? | Whether the operation may have committed; idempotency, status lookup, and reconciliation |
| How do you prevent prompt injection? | Data/instruction boundaries and enforced tool permissions; residual failure tests |
| What does MCP solve? | A tool/resource interface; protocol version and authorization; no automatic trust guarantee |
| What does A2A solve? | Interoperability between agent services; task and artifact contracts; delegated authority |
| How do you know it is correct? | Final state, evidence, prohibited effects, repeated trials, and calibrated grading |
| What if the model or tool is unavailable? | Backpressure, retry limits, saved progress, fallback, and user-visible status |
| How do you reduce cost? | Profile first; remove unnecessary work; cache safely; route with measured quality |
| Can a run resume safely? | Durable execution state plus a separate action ledger and downstream effect semantics |

## Example interview questions

1. How would a support agent answer order questions and propose refunds?
2. How would a research assistant produce a cited report from private and public sources?
3. How would a coding agent turn an issue description into a patch for review?
4. How would an incident assistant diagnose failures and propose remediation?
5. How would a travel assistant search options and obtain approval before booking?
6. How would a data analysis agent query tenant data and produce reproducible charts?

The first four questions have [worked case studies](case-studies.md). Travel and data analysis agents involve related questions about run contracts, tool permissions, and evaluation.

## Self-assessment rubric

The rubric uses three levels for each dimension: **0** (missing), **1** (named), and **2** (explained with a concrete mechanism and tradeoff).

| Dimension | Evidence for a 2 |
| --- | --- |
| Requirements | Observable success and explicit non-goals/actions |
| Architecture | Clear control flow and a justified baseline |
| Data and context | Access boundaries, retrieval quality, freshness, and state ownership |
| Tool execution | Preconditions, receipts, approval, and retry semantics |
| Reliability | Recovery from a crash and an ambiguous write outcome |
| Safety | Enforced permissions and an untrusted-content test |
| Evaluation | Task-level graders, repeated trials, and failure categories |
| Scale and cost | Numerical estimates, bottleneck, and resource limits |
| Communication | Assumptions and alternatives stated clearly |

The rubric emphasizes concrete mechanisms, failure behavior, and the evidence behind design choices.
