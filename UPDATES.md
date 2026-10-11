# Recent developments in agentic system design

[Home](README.md) · [Research papers](resources/papers.md) · [Frameworks](resources/frameworks.md)

Selected research developments, protocol releases, and platform changes, with their implications for system design. Dates refer to the publication, submission, or release identified by each source.

## Dated developments

| Date | Development and primary source | Status | Design implication |
| --- | --- | --- | --- |
| 2026-10-06 | [HERMES / modular executable Dev-Primitives](https://arxiv.org/abs/2610.07832) | New research preprint | Investigate component-level interfaces for repository work; reproduce the cost and quality tradeoff before adopting the architecture. |
| 2026-09-08 | [SWE-Bench Pro Verified](https://arxiv.org/abs/2609.08149) | Research; revised September 16 | Inspect task quality and evaluation leakage. Keep this benchmark distinct from SWE-bench Verified and report the exact variant. |
| 2026-08-22 | [Updated MCP roadmap](https://blog.modelcontextprotocol.io/posts/mcp-roadmap/) | Roadmap | Track messaging, transport, identity, and SDK work; use the released specification for compatibility commitments. |
| 2026-07-31 | [LoopsBench](https://arxiv.org/abs/2608.00267) | Research benchmark; revised August 10 | Evaluate dependency order, regressions during sustained execution, and final artifacts. |
| 2026-07-28 | [MCP specification revision](https://blog.modelcontextprotocol.io/posts/2026-07-28/) | Released specification | Revisit session assumptions: stateless core, Multi Round-Trip Requests, routing/cache changes, and Tasks as an extension. Test the clients and servers you actually deploy. |
| 2026-06-03 | [OpenAI Agent Builder deprecation](https://developers.openai.com/api/docs/deprecations) | Deprecated; shutdown scheduled for 2026-11-30 | Plan migration for existing workflows and consult current runtime options for new applications. |
| 2026-05-25 | [How Anthropic contains Claude across products](https://www.anthropic.com/engineering/how-we-contain-claude) | Engineering report | Review sandbox and network boundaries and the maximum effect of a failure. |
| 2026-04-08 | [Scaling Managed Agents](https://www.anthropic.com/engineering/managed-agents) | Engineering report | Separate session history, agent control flow, and execution environments when designing long-running work. |
| 2026-04-02 | [Microsoft Agent Framework 1.0 GA, reported in the BUILD recap](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-at-build-2026-announce/) | Framework release | Evaluate the successor to AutoGen and Semantic Kernel; verify newer feature maturity separately. |
| 2026-03-24 | [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) | Engineering report | Treat the harness and verification loop as variables to evaluate alongside model choice. |
| 2026-02-18 | [Towards a Science of AI Agent Reliability](https://arxiv.org/abs/2602.16666) | Research; revised June 2 | Measure repeatability, perturbation sensitivity, and failure consequences alongside accuracy. |
| 2026-01-09 | [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | Engineering guide | Build task and trajectory evaluation into the development cycle. |

## Runtime and protocol changes

| Area | Change or capability | Design consideration |
| --- | --- | --- |
| OpenAI runtimes | [Documentation](https://developers.openai.com/api/docs/guides/agents) distinguishes the managed Agents API, Agents SDK, and Responses API | Choose based on ownership of control flow, state, and execution. |
| Microsoft AutoGen | [Repository](https://github.com/microsoft/autogen) states maintenance mode and recommends Microsoft Agent Framework for new work | Read migration guidance before copying an older tutorial. AG2 is a separate project. |
| A2A | [Specification](https://a2a-protocol.org/latest/specification/) documents 1.0 behavior and changes from 0.3 | Pin supported versions and test event/part serialization and version handling. |
| Agent Skills | [Specification](https://agentskills.io/specification) defines portable instructions and resources with progressive loading | Assess instruction provenance and execution permissions independently of packaging. |

## Engineering and release sources

[Anthropic engineering](https://www.anthropic.com/engineering), [OpenAI agent documentation](https://developers.openai.com/api/docs/guides/agents), [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/), and [MCP announcements](https://blog.modelcontextprotocol.io/) cover implementation guidance and ecosystem developments. Paper submission histories document initial publications and later revisions.
