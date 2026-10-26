# Frameworks, SDKs, and platforms

[Home](../README.md) · [Architecture](../docs/architecture.md) · [Tools and protocols](../docs/tools-and-protocols.md)

Frameworks, SDKs, and platforms offer different approaches to control flow, state, tool execution, and deployment. These capabilities shape the tradeoffs between implementations.

## Choose by responsibility

| Capability | Design considerations |
| --- | --- |
| Own the agent loop | Tool dispatch, state access, structured outputs, stopping conditions, model adapters |
| Explicit workflow control | Graph/state-machine semantics, checkpoints, interrupts, recovery, replay |
| Delegate work | Typed handoffs, scoped tools, shared-state ownership, budgets, cancellation |
| Run code or use computers | Sandbox boundary, filesystem/network controls, artifacts, approval hooks |
| Operate a service | Authentication, tenancy, queues, tracing, deployment, upgrades, exportability |
| Adopt a hosted runtime | Responsibility split, retention, region availability, quotas, recovery semantics, cost |

A representative recovery scenario spans evidence retrieval, a proposed write, approval, a worker crash, and resumption. Its outcome depends on checkpoint behavior, approval persistence, and duplicate-effect prevention.

## General-purpose orchestration and SDKs

| Project | Approach | Design question |
| --- | --- | --- |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Stateful graph orchestration and durable execution | How will state, interrupts, and replay map to your business workflow? |
| [Google ADK](https://github.com/google/adk-python) | Agent and workflow components with development/evaluation tooling | Does its session and deployment model fit your application? |
| [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/) | Agents and workflows succeeding AutoGen and Semantic Kernel | What changes when migrating your existing orchestration? |
| [OpenAI Agents SDK](https://developers.openai.com/api/docs/guides/agents/quickstart) | Code-defined agents, tools, and orchestration | Which state, execution, and deployment responsibilities remain in your app? |
| [Claude Agent SDK](https://code.claude.com/docs/en/agent-sdk/overview) | Programmable access to Claude Code's agent capabilities | Do its tools, runtime, and permission model fit the workload? |
| [Pydantic AI](https://github.com/pydantic/pydantic-ai) | Typed agent inputs, dependencies, tools, and outputs | Can you enforce the data contracts your application needs? |
| [Strands Agents / Harness SDK](https://github.com/strands-agents/harness-sdk) | Model-driven agents and configurable harnesses | Do assembled harness defaults fit, or do you need control of the loop? |
| [CrewAI](https://github.com/crewAIInc/crewAI) | Agent crews and workflow flows | Which stages should be explicit flows versus delegated work? |
| [Agno](https://github.com/agno-agi/agno) | Agents, teams, and runtime/platform components | Which components are libraries and which become services you operate? |
| [Mastra](https://github.com/mastra-ai/mastra) | TypeScript application and agent framework | How well does it integrate with your TypeScript service and state model? |
| [smolagents](https://github.com/huggingface/smolagents) | Compact tool-using agents, including code-based actions | Where and with what permissions will generated code execute? |
| [AgentScope](https://github.com/agentscope-ai/agentscope) | Agent programming and multi-agent applications | How are messages, tools, and execution observed and controlled? |
| [AG2](https://github.com/ag2ai/ag2) | Multi-agent conversations and orchestration | Does conversation-based coordination fit your task? |

AG2 and Microsoft's AutoGen are separate projects. Do not apply one project's release or maintenance status to the other.

## Platforms, integrations, and managed execution

| Project | What it adds | Boundary to review |
| --- | --- | --- |
| [Dify](https://github.com/langgenius/dify) | Visual application workflows, agents, and retrieval pipelines | Hosting, extensions, data access, and workflow portability |
| [Accenture AI Refinery](https://sdk.airefinery.accenture.com/ai_refinery_101/) | Enterprise agent development platform and SDK | Platform dependencies, access requirements, and deployment model |
| [Microsoft 365 Agents SDK](https://learn.microsoft.com/en-us/microsoft-365/agents-sdk/agents-sdk-overview) | Agent integration into Microsoft 365 and other channels | Channel/identity integration versus the reasoning runtime |
| [OpenAI Agents API](https://developers.openai.com/api/docs/guides/agents-api/overview) | Managed Codex harness with sessions and execution environments | Hosted versus self-hosted sandbox responsibilities and tool permissions |
| [Claude Managed Agents architecture](https://www.anthropic.com/engineering/managed-agents) | Managed long-running execution separating session, harness, and sandbox | Which state and runtime behavior the service owns |
| [Amazon Bedrock AgentCore](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/what-is-bedrock-agentcore.html) | Services for agent runtime, tools, memory, identity, and observability | Which services you need and their IAM, quota, and data boundaries |
| [Google Cloud agent architecture components](https://docs.cloud.google.com/architecture/choose-agentic-ai-architecture-components) | A guide to runtime, state, and memory choices on Google Cloud | Managed services versus the components you operate |
| [Scalekit AgentKit](https://docs.scalekit.com/agentkit/overview/) | Managed integration layer: per-user OAuth grants, a token vault outside the agent, 600+ connectors and 35,000+ tools callable from SDKs or any MCP client, with tool exposure scoped per agent role | Who holds user credentials, how tool scope is enforced outside the prompt, and what the hosted layer logs |

## Specialized systems and application examples

| Project | Focus |
| --- | --- |
| [Agent S](https://github.com/simular-ai/Agent-S) | Computer-use agent architecture |
| [MetaGPT](https://github.com/FoundationAgents/MetaGPT) | Role-based multi-agent software-development workflows |
| [YYLO](https://github.com/yylo-dev/yylo) | Command-line coding-agent orchestration, isolated task workspaces, validation boundaries, and recorded repository changes |
| [Darkmoon](https://github.com/ASCIT31/Dark-Moon) | A specialized security-testing application; assess scope controls and evidence handling in authorized environments |

## Project status and migration

- **AutoGen:** the [Microsoft repository](https://github.com/microsoft/autogen) states that it is in maintenance mode and directs new development toward Microsoft Agent Framework.
- **Microsoft Agent Framework:** Microsoft's [BUILD 2026 report](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-at-build-2026-announce/) dates 1.0 general availability to April 2, 2026. Check feature-specific release status rather than assuming every newer extension shares it.
- **OpenAI Agent Builder:** [deprecated June 3, 2026, with shutdown scheduled for November 30, 2026](https://developers.openai.com/api/docs/deprecations). Follow the linked migration guidance for existing workflows and consult current runtime options for new applications.

For a dated record of these changes, see [updates](../UPDATES.md).
