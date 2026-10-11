# Research papers by design question

[Home](../README.md) · [Guides](guides.md) · [Recent developments](../UPDATES.md)

Years below refer to the initial preprint submission or posting. Links lead to abstract pages with version history. Check the venue, artifacts, baselines, compute budget, and limitations when assessing results.

The catalog groups foundational work and later research by design question.

## Foundations: how does an agent act and improve?

| Paper | Year | Topic |
| --- | --- | --- |
| [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) | 2022 | Interleaving reasoning, actions, and observations |
| [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) | 2023 | Using verbal feedback across attempts |

## Surveys: how do the pieces fit together?

| Paper | Year | Topic |
| --- | --- | --- |
| [Agentic Large Language Models, a survey](https://arxiv.org/abs/2503.23037) | 2025 | A map of reasoning, action, and interaction research |
| [Large Language Model Agent: A Survey on Methodology, Applications and Challenges](https://arxiv.org/abs/2503.21460) | 2025 | A broad methodology and application taxonomy |
| [A Survey of Self-Evolving Agents](https://arxiv.org/abs/2507.21046) | 2025 | What aspects of agents can change through experience |
| [Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG](https://arxiv.org/abs/2501.09136) | 2025 | Retrieval as part of a decision loop |
| [Multi-Agent Collaboration Mechanisms: A Survey of LLMs](https://arxiv.org/abs/2501.06322) | 2025 | Coordination mechanisms and collaboration choices |
| [A survey of agent interoperability protocols: MCP, ACP, A2A, and ANP](https://arxiv.org/abs/2505.02279) | 2025 | Historical protocol taxonomy; use current specifications for implementation |
| [Agentic AI Frameworks: Architectures, Protocols, and Design Challenges](https://arxiv.org/abs/2508.10146) | 2025 | Connections between framework design and protocol choices |
| [Architectures for Building Agentic AI](https://arxiv.org/abs/2512.09458) | 2025 | Architectural organization of agent systems |
| [Agentic Design Patterns: A System-Theoretic Framework](https://arxiv.org/abs/2601.19752) | 2026 | A systems perspective on agent design patterns |
| [LLM Agents: A Survey](https://www.preprints.org/manuscript/202608.0265/v1) | 2026 | A component-based survey of planning, memory, tools, and coordination, with evaluation and safety coverage; preprint |

## Orchestration: which workflow and topology should we use?

| Paper | Year | Topic |
| --- | --- | --- |
| [AFlow: Automating Agentic Workflow Generation](https://arxiv.org/abs/2410.10762) | 2024 | Searching over workflow designs |
| [Multi-Agent Design: Optimizing Agents with Better Prompts and Topologies](https://arxiv.org/abs/2502.02533) | 2025 | Joint prompt and topology optimization |
| [Weak-for-Strong: Training Weak Meta-Agent to Harness Strong Executors](https://arxiv.org/abs/2504.04785) | 2025 | Separating orchestration from executor capability |
| [FlowReasoner: Reinforcing Query-Level Meta-Agents](https://arxiv.org/abs/2504.15257) | 2025 | Adapting orchestration to individual queries |
| [MetaAgent: Automatically Constructing Multi-Agent Systems Based on Finite State Machines](https://arxiv.org/abs/2507.22606) | 2025 | Explicit state-machine structure in generated systems |
| [On the Role of Feedback in Test-Time Scaling of Agentic AI Workflows](https://arxiv.org/abs/2504.01931) | 2025 | How feedback changes the value of extra inference |
| [Budget-Aware Tool Use Enables Effective Agent Scaling](https://arxiv.org/abs/2511.17006) | 2025 | Resource-constrained tool use |
| [Towards a Science of Scaling Agent Systems](https://arxiv.org/abs/2512.08296) | 2025 | Evaluating scaling and coordination tradeoffs |
| [CORAL: Towards Autonomous Multi-Agent Evolution for Open-Ended Discovery](https://arxiv.org/abs/2604.01658) | 2026 | Evolving multi-agent systems for discovery tasks |

## Context and harnesses: what should the runtime remember and control?

| Paper | Year | Topic |
| --- | --- | --- |
| [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) | 2025 | Linked, evolving memory organization |
| [A Practical Guide for Designing, Developing, and Deploying Production-Grade Agentic AI Workflows](https://arxiv.org/abs/2512.08769) | 2025 | Production workflow design considerations |
| [RewardHarness: Self-Evolving Agentic Post-Training](https://arxiv.org/abs/2605.08703) | 2026 | Evolving tools and skills for image-edit preference judgments; a specialized reward-modeling study |
| [Harness Engineering: Anatomy, Architecture, and Evolution of Coding Agents — A Source-Code Study of Eleven Systems](https://arxiv.org/abs/2609.00006) | 2026 | Comparing runtime designs in a specific corpus of coding systems |
| [The Agent Loop: A Survey of Control Strategies, Skills, and Harnesses for LLM Agents](https://ssrn.com/abstract=7186738) | 2026 | Control strategies, termination, recovery, skills, and harness design; preprint with an [author-hosted reading copy](https://github.com/js-lee-AI/awesome-agent-loop-papers/blob/main/paper/the-agent-loop-survey.pdf) |
| [Harness Engineering for Software Engineering via Modular Executable Dev-Primitives](https://arxiv.org/abs/2610.07832) | 2026 | HERMES and component-level agent interfaces; new preprint submitted October 6 |

## Evaluation: what are we actually measuring?

| Paper | Year | Topic |
| --- | --- | --- |
| [GAIA: a benchmark for General AI Assistants](https://arxiv.org/abs/2311.12983) | 2023 | General assistant evaluation involving reasoning and tools |
| [Survey on Evaluation of LLM-based Agents](https://arxiv.org/abs/2503.16416) | 2025 | Evaluation dimensions and methodology |
| [MultiAgentBench: Evaluating the Collaboration and Competition of LLM agents](https://arxiv.org/abs/2503.01935) | 2025 | Measuring behavior across interacting agents |
| [ClawBench: Can AI Agents Complete Everyday Online Tasks?](https://arxiv.org/abs/2604.08523) | 2026 | Live web workflows with an interception layer for final submissions |
| [PerspectiveGap: A Benchmark for Multi-Agent Orchestration Prompting](https://arxiv.org/abs/2606.08878) | 2026 | Information selection when instructing other agents |
| [LoopsBench: From Harness Engineering to Loop Engineering in Coding Agent Evaluation](https://arxiv.org/abs/2608.00267) | 2026 | Dependencies and regression obligations during sustained development |
| [SWE-Bench Pro Verified: A Reliable Benchmark for Software Engineering Agents](https://arxiv.org/abs/2609.08149) | 2026 | Benchmark quality and verification in a separate SWE-Bench Pro line; do not conflate it with SWE-bench Verified |

See the [benchmark selection guide](../docs/evaluation.md#benchmark-selection) for project links and limitations.

## Safety and attribution: how can we understand failures?

| Paper | Year | Topic |
| --- | --- | --- |
| [Because we have LLMs, we Can and Should Pursue Agentic Interpretability](https://arxiv.org/abs/2506.12152) | 2025 | A research direction for agent-assisted interpretability |
| [AgenTracer: Who Is Inducing Failure in the LLM Agentic Systems?](https://arxiv.org/abs/2509.03312) | 2025 | Attributing failures within an agent system |
| [Toward a Safe Internet of Agents](https://arxiv.org/abs/2512.00520) | 2025 | Safety questions for interconnected agents |
| [Towards a Science of AI Agent Reliability](https://arxiv.org/abs/2602.16666) | 2026 | Consistency, robustness, predictability, and safety beyond average success |

## Research comparison dimensions

Research comparisons depend on the design question, baseline, task and environment assumptions, total inference/training budget, and availability of code and data. Model, tool, and runtime changes can each contribute to reported gains. The evaluation metric determines which aspects of success those gains describe.
