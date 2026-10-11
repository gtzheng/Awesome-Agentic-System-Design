# Architecture and orchestration

[Home](../README.md) · [Learning roadmap](learning-roadmap.md) · [Context and memory](context-and-memory.md)

Start with the task, its success criterion, and its permitted actions. Use a fixed workflow when the steps are known. Introduce model-driven control where choosing the next action requires judgment. The workflow/agent distinction and common patterns are introduced in [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents).

The recommendations below are design heuristics. Validate them against your workload.

## Choose the smallest useful control structure

| Pattern | Good fit | Main tradeoff | Failure to test |
| --- | --- | --- | --- |
| Single model call | Classification, extraction, short-form drafting | Low complexity; limited adaptation | Unsupported output or malformed fields |
| Fixed workflow | Known stages with explicit dependencies | Predictable execution; branches must be designed | Bad intermediate results propagate |
| Router | Task classes need different tools or policies | Specialized handling; routing can fail | Wrong route gains unnecessary permissions |
| Single agent with tools | Next action depends on observations | Flexible path; variable cost and termination | Repeated calls without progress |
| Parallel workers | Independent subtasks or checks | Lower elapsed time; aggregation overhead | Duplicated work or incompatible answers |
| Planner and executors | Decomposable tasks with clearly defined deliverables | Specialization; coordination overhead | A plan omits a dependency |
| Generator and verifier | Outputs have executable tests or a rubric | Correction opportunities; verifier can be wrong | Both stages share a mistaken assumption |
| Human checkpoint | Ambiguous or consequential decisions | Oversight; queueing and abandonment | Approval applies to an outdated action |

Combine patterns when justified. A deterministic support workflow can contain an agent that searches policies, followed by a deterministic eligibility check.

## Define a run contract

Write this before choosing a framework:

```text
Input: request, authenticated principal, tenant, supplied artifacts
Goal: observable outcome and required evidence
Allowed actions: explicit read/write capabilities and resource scopes
State: run ID, status, plan, evidence, action ledger, remaining budget
Limits: deadline, turns, tool calls, spend, delegation depth
Completion: verified outcome, clarification, human handoff, or failure
Output: answer/artifact, evidence, action receipts, limitations
```

Separate a model's proposed action from the runtime's authority to execute it. Schema validation checks shape; application code must also check ownership, preconditions, and authorization.

## An agent loop with execution limits

The following pseudocode illustrates the control flow:

```text
load or create durable run state
while the run is active:
    check cancellation, deadline, and remaining budget
    build context from current state and permitted evidence
    ask the model for an answer, clarification, or proposed action
    validate the proposed transition
    if an action is proposed:
        authorize it and obtain any required approval
        record intent with a stable logical operation ID
        execute or reconcile using the operation's idempotency contract
        persist the result, receipt, and updated state
    else:
        verify completion or persist the clarification/handoff
return the recorded outcome
```

The difficult gap is between an external action committing and the worker saving its result. A checkpoint alone cannot close it. See [recovery semantics](production-and-safety.md#durable-execution-and-side-effects).

## When multiple agents help

Test delegation when subtasks have separable contexts, tools, or expertise and can be evaluated independently. A model playing a reviewer role is not automatically an independent verifier.

Each delegated task needs:

- A clearly defined objective, inputs, allowed data, and expected artifact.
- A deadline and a share of the parent run's budget.
- A typed result with evidence, status, and unresolved issues.
- Ownership of writes and a rule for resolving conflicting outputs.
- Cancellation, retry, and escalation behavior.

Have one owner merge shared state, or use transactional/versioned updates. Give workers scoped capabilities; delegation must not silently expand authority. Evaluate orchestration mistakes separately from worker mistakes. [PerspectiveGap](https://arxiv.org/abs/2606.08878) studies supplying appropriate information in orchestration prompts.

## Plans, feedback, and termination

A plan is a hypothesis. Store completed steps and evidence separately from proposed steps. Replan when observations invalidate a dependency.

Prefer verifiable feedback: tests, database state, citations, schema checks, or a human decision. Critique without new evidence can repeat the same error. [Reflexion](https://arxiv.org/abs/2303.11366) explores feedback across attempts; [scaling agent systems](https://arxiv.org/abs/2512.08296) examines architectural tradeoffs empirically.

Define stop conditions for success, insufficient evidence, repeated failure, exhausted resources, and cancellation. An honest partial result with recorded progress is a valid outcome.

**Design question:** in a research assistant, which steps are fixed, which require model judgment, and how does parallel work affect coverage at the same total budget?
