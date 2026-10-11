# Guides, books, and engineering reports

[Home](../README.md) · [Learning roadmap](../docs/learning-roadmap.md) · [Research papers](papers.md)

Books, technical guides, specifications, and engineering reports grouped by subject.

## Foundations and design patterns

| Resource | Coverage |
| --- | --- |
| [Building effective agents — Anthropic](https://www.anthropic.com/engineering/building-effective-agents) | Workflow and agent pattern vocabulary |
| [Agents — Google / Kaggle](https://www.kaggle.com/whitepaper-agents) | Models, tools, and orchestration fundamentals |
| [A Practical Guide to Building Agents — OpenAI](https://cdn.openai.com/business-guides-and-resources/a-practical-guide-to-building-agents.pdf) | An introductory design guide; use current API docs for implementation details |
| [Agentic Design Patterns — Antonio Gulli, Springer](https://link.springer.com/book/10.1007/978-3-032-01402-3) | A book-length pattern reference; full text may require purchase or institutional access |
| [Designing Agentic AI Systems, Part 1: Agent Architectures — Vectorize](https://vectorize.io/blog/designing-agentic-ai-systems-part-1-agent-architectures) | A practical introduction to architectural choices |
| [7 Practical Design Patterns for Agentic Systems — MongoDB](https://www.mongodb.com/resources/basics/artificial-intelligence/agentic-systems) | Patterns illustrated from a data-platform perspective |

## Context, tools, and collaboration

| Resource | Coverage |
| --- | --- |
| [Effective context engineering for AI agents — Anthropic](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Selecting and maintaining useful context |
| [Writing effective tools for AI agents — Anthropic](https://www.anthropic.com/engineering/writing-tools-for-agents) | Tool interfaces and evaluations |
| [How we built our multi-agent research system — Anthropic](https://www.anthropic.com/engineering/multi-agent-research-system) | A concrete research-agent architecture and its tradeoffs |
| [Agent Skills specification](https://agentskills.io/specification) | Packaging reusable task instructions and supporting resources |
| [MCP specification, 2026-07-28](https://modelcontextprotocol.io/specification/2026-07-28) | The versioned tool/resource protocol reference |
| [A2A specification](https://a2a-protocol.org/latest/specification/) | Agent-service interoperability and migration details |

## Long-running execution, evaluation, and safety

| Resource | Coverage |
| --- | --- |
| [Effective harnesses for long-running agents — Anthropic](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) | Maintaining progress across context windows |
| [Harness design for long-running application development — Anthropic](https://www.anthropic.com/engineering/harness-design-long-running-apps) | Generator/evaluator arrangements and harness iteration |
| [Scaling Managed Agents — Anthropic](https://www.anthropic.com/engineering/managed-agents) | Separating session storage, harness, and sandbox responsibilities |
| [Demystifying evals for AI agents — Anthropic](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | Designing an evaluation program for an agent system |
| [How we contain Claude across products — Anthropic](https://www.anthropic.com/engineering/how-we-contain-claude) | Containment boundaries and practical security failure modes |
| [A Guide to Architecting Secure Enterprise AI Agents with MCP Servers — IBM, verified by Anthropic](https://www.ibm.com/downloads/documents/us-en/1443d5dd174f42e6) | Enterprise integration and security architecture; compare protocol details with the current specification |

## Platform architecture references

| Resource | Coverage |
| --- | --- |
| [OpenAI agents runtime overview](https://developers.openai.com/api/docs/guides/agents) | Distinguishing managed Agents API, application-owned Agents SDK, and direct Responses integration |
| [Microsoft Agent Framework overview](https://learn.microsoft.com/en-us/agent-framework/overview/) | Agents, workflows, and migration from earlier Microsoft frameworks |
| [Google Cloud: choose agentic AI architecture components](https://docs.cloud.google.com/architecture/choose-agentic-ai-architecture-components) | Runtime and state-management decisions on Google Cloud |
| [Amazon Bedrock AgentCore overview](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html) | Managed operational components around an agent |
| [What is Agent Bricks? — Databricks](https://docs.databricks.com/aws/en/agents/concepts) | Agent Bricks concepts and application development on Databricks |
| [The Big Book of Generative AI — Databricks](https://www.databricks.com/resources/ebook/big-book-generative-ai) | GenAI application background; access may require registration |

Related pages: [framework catalog](frameworks.md) and [learning roadmap](../docs/learning-roadmap.md).
