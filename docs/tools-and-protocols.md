# Tools, skills, and interoperability

[Home](../README.md) · [Context and memory](context-and-memory.md) · [Production and safety](production-and-safety.md)

Tools turn model output into effects. Design their contracts with the same care as a public API, then evaluate whether the model can select and use them correctly.

## A tool contract

| Field | Example | Why it matters |
| --- | --- | --- |
| Purpose | `get_order_status` retrieves one authenticated customer's order | Distinguishes it from search, cancellation, and refund tools |
| Input schema | Order ID; reject unknown fields | Limits ambiguity and malformed requests |
| Authorization | Server derives tenant and user from authenticated context | A model-supplied customer ID is not proof of ownership |
| Preconditions | Order exists and belongs to the caller | Valid JSON can still describe an invalid action |
| Side effects | Read-only, reversible write, or consequential write | Determines approval and retry policy |
| Result | Status, structured data, source timestamp, receipt | Lets the agent distinguish success from an attempted action |
| Errors | Invalid input, denied, not found, transient, unknown outcome | Makes recovery specific to the failure |
| Execution limits | Timeout, rate limit, output size, cancellation support | Bounds resource use |
| Idempotency | Stable operation ID for a logical refund | Avoids duplicate effects after retries |

Prefer a small set of purposeful tools over many overlapping operations. Return the relevant fields and handles to large artifacts. Include units and timestamps where interpretation depends on them. [Writing effective tools](https://www.anthropic.com/engineering/writing-tools-for-agents) provides examples of tool design and evaluation.

## Different standards solve different problems

Follow a versioned specification when implementing wire behavior; a link labeled `latest` can change.

| Interface | Main boundary | What to study | What remains your responsibility |
| --- | --- | --- | --- |
| Function/tool calling | Model output to application functions | Schemas, execution, result messages | Argument validation, authorization, retries, and effects |
| [Model Context Protocol (MCP)](https://modelcontextprotocol.io/specification/2026-07-28) | An agent host/client to tools, resources, and prompts exposed by servers | Capabilities, transport, authorization, extensions | Trusting a server, scoping access, and validating its results |
| [Agent2Agent (A2A)](https://a2a-protocol.org/latest/specification/) | Independently implemented agent services | Agent Cards, tasks, messages, artifacts, streaming | Delegation policy, identity, tenancy, and outcome verification |
| [Agent Skills](https://agentskills.io/specification) | Portable task instructions and supporting files | `SKILL.md` metadata and progressive loading | Trust, permissions, script isolation, and runtime compatibility |

A skill can explain a procedure that uses an MCP tool. An agent service can expose work through A2A and use tools internally. These interfaces can coexist; none replaces the application's control flow or permission system.

## MCP version awareness

The **2026-07-28** revision introduces a stateless core, Multi Round-Trip Requests, routing headers, cacheable catalogs, and a formal extension mechanism. Tasks move into an extension. Older tutorials may describe earlier session and transport assumptions. Consult the [release explanation](https://blog.modelcontextprotocol.io/posts/2026-07-28/) and the versioned specification together.

Before an upgrade, test client/server compatibility, capabilities, authorization, error handling, and any task or UI extensions your application uses. Stateless protocol handling does not make your business process stateless.

## A2A version awareness

The A2A specification documents **1.0** behavior and migration from 0.3, including version headers and changed representations for parts and events. Verify the actual version supported by both endpoints. An Agent Card advertises an interface; your application still needs a trust decision and an authorization policy. See the [A2A specification and migration appendix](https://a2a-protocol.org/latest/specification/).

Older papers use several meanings of “ACP.” Spell out the protocol name and version before comparing implementations; the [2025 interoperability survey](https://arxiv.org/abs/2505.02279) provides historical context. Check current specifications for compatibility.

## Large tool catalogs and code execution

For a large catalog, consider discovering relevant tools before presenting complete schemas. Evaluate missed tools and extra discovery latency. Cache catalogs with version and permission scope; never share a privileged catalog across tenants accidentally.

Code execution can combine many operations and manipulate large results efficiently, but moves more behavior into an execution environment. Apply filesystem, network, credential, time, and resource controls. Keep durable receipts for external writes regardless of whether a tool call originated directly from the model or from generated code.

**Design question:** when a refund request times out after committing, how can the caller establish the outcome and retrieve the original receipt?
