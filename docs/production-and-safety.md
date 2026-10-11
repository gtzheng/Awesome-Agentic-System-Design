# Production, reliability, and safety

[Home](../README.md) · [Tools and protocols](tools-and-protocols.md) · [Evaluation](evaluation.md)

An agent is a stateful application that can encounter untrusted input and cause external effects. The following design checklist is a starting point for implementation and review. Choose controls based on the application's actual data, actions, and failure consequences.

## Durable execution and side effects

Persist runs separately from worker processes. A useful lifecycle is `queued → running → waiting_for_input/approval → running → succeeded/failed/cancelled`. Record terminal outcomes explicitly and use leases or equivalent coordination to prevent competing workers from owning the same run.

For an external write:

1. Validate identity, authorization, preconditions, and the current approval.
2. Persist intent with a stable ID for the logical operation.
3. Send that ID as an idempotency key when the downstream service supports it.
4. Persist the receipt and updated run state.
5. After a crash or ambiguous timeout, query/reconcile the operation before deciding to retry.

Checkpointing does not guarantee exactly-once external effects. If the service has neither idempotency nor a reliable status lookup, a timeout can remain ambiguous. Stop automatic retries and escalate or reconcile through a domain-specific process. A compensating action may also be required; compensation is not equivalent to an atomic rollback.

Use a retry limit with backoff and jitter for transient failures. Avoid retrying invalid requests, permission denials, or unknown write outcomes as if they were ordinary network failures. Propagate cancellation to queued and delegated work while accounting for actions already in flight.

For a concrete runtime design separating sessions, harnesses, and execution environments, see [Anthropic's Managed Agents engineering report](https://www.anthropic.com/engineering/managed-agents).

## Enforce trust boundaries

| Boundary | Typical failure | Control to design and test |
| --- | --- | --- |
| Retrieved content → model | A document contains instructions to exfiltrate data | Preserve provenance; treat content as data; enforce destination and tool restrictions outside the model |
| Model → tool | Plausible but unauthorized arguments | Authenticate the caller, validate arguments, and enforce resource-level policy |
| Tool server → runtime | A compromised server returns misleading content | Allowlisted integrations, output validation, scoped credentials, and audit trails |
| Generated code → environment | Code reads secrets or reaches unrestricted networks | Isolated execution, least privilege, egress controls, and resource limits |
| Agent → another agent | Delegation broadens data or action access | Explicit capability scopes and typed task/result contracts |
| Approval → action | Parameters change after approval | Bind approval to the exact action, resource, parameters, and expiry; revalidate before execution |
| Tenant → shared infrastructure | Caches, memory, or traces leak another user's data | Scope every storage and retrieval path, including derived data |

Prompt instructions and model-based filters can reduce risk, but they do not replace authorization or isolation. Test controls against malicious user prompts, tool outputs, and retrieved documents. The [MCP specification](https://modelcontextprotocol.io/specification/2026-07-28) and [IBM enterprise MCP guide](https://www.ibm.com/downloads/documents/us-en/1443d5dd174f42e6) provide protocol and deployment references.

## Human involvement

Show the proposed action, target, effect, and relevant evidence. Offer edit, approve, reject, and escalate paths where appropriate. Persist pending approval so a worker restart does not lose it. Recheck permissions and business state after a long approval delay.

Specify what happens when nobody responds. A timeout should reach a defined state; it must not imply approval. Measure review workload and unnecessary interruptions alongside automated success.

## Observe the system

Correlate each run, model call, tool call, delegated task, approval, and artifact. Record versioned configuration, elapsed time, token/tool usage, errors, and externally visible effects. Use structured events that permit failure attribution.

Record observable actions and evidence; do not require access to hidden model reasoning. Redact credentials and sensitive fields, restrict access to traces, and apply retention policies to raw and derived data. Replay against snapshots or mocks when a live replay would repeat side effects.

## Budget latency and cost

Track cost at the run level, including failed attempts, tool fees, execution environments, and delegation. Streaming improves time to first visible output but may not reduce completion time.

```text
run cost ≈ sum(model calls + tool charges + execution cost)
cost per accepted task = total evaluated cost / accepted tasks
serial latency ≈ queue delay + sum(model and tool durations)
parallel stage latency ≈ slowest required branch + coordination overhead
```

Set a maximum spend, deadline, turn count, and delegation depth. Reserve part of the budget for verification and a useful final response. Control concurrency and queueing to respect downstream quotas. Cache only where freshness, identity, and permission scopes permit reuse.

Route easier tasks to cheaper configurations only after measuring quality on those tasks. Re-evaluate after changing models, prompts, tool descriptions, or retrieval. A cheaper request can produce a more expensive successful outcome if it requires more retries.

## Release and operate

Pin model identifiers where supported, dependencies, prompt versions, tool schemas, and protocol versions. Use an offline regression set, a limited rollout, and a rollback path. Maintain a kill switch for writes and a fallback such as read-only answers or human handling.

Before launch, demonstrate recovery from a worker crash, provider outage, exhausted budget, stale approval, and tool timeout after a committed write. Verify that incidents produce enough evidence to identify the failing component.

**Design question:** during an outage in a purchase or refund workflow, which effects are known, which remain uncertain, and who owns reconciliation?
