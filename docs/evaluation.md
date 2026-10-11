# Evaluation and benchmarks

[Home](../README.md) · [Architecture](architecture.md) · [Research papers](../resources/papers.md)

Evaluate the **model, prompts, tools, runtime, and environment together**. A fluent answer does not prove a task was completed. A tool call that returned successfully does not prove the action was appropriate. [Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) covers evaluation terminology and methodology.

## Build an evaluation set before optimizing

Collect representative tasks with initial state, permitted actions, expected outcomes, and failure severity. Include ordinary cases, ambiguity, unavailable tools, stale evidence, malicious inputs, and actions requiring approval.

For each case, store:

```text
case ID and task category
input, identity, initial environment, and permitted data
expected final state and prohibited changes
grader and human review rubric
model, prompt, tool, runtime, and dataset versions
budget, timeout, sampling settings, and trial count
trace, artifacts, action receipts, cost, and elapsed time
```

Keep development cases separate from held-out regression cases. Add production failures as new cases, but do not tune indefinitely against the test set. Reset the environment between trials so earlier writes cannot help later runs.

## Measure more than completion

| Dimension | Example measure | What it tells you |
| --- | --- | --- |
| Outcome | Fraction of eligible tasks completed correctly | Whether the system solves the intended task |
| Safety / policy | Unauthorized effects; severity of violations | Whether success hid an unacceptable action |
| Grounding | Supported claims and citation correctness | Whether an answer follows the evidence |
| Consistency | Success across repeated trials | Whether one successful demo is repeatable |
| Robustness | Performance after realistic perturbations | Sensitivity to phrasing, state, tool errors, or distractions |
| Recovery | Duplicate effects, resume success, lost progress | Behavior under operational faults |
| Efficiency | Cost per accepted task; p50/p95 latency | The cost of useful work, including failed attempts |
| User experience | Unnecessary clarifications, handoffs, abandonment | Whether the workflow remains usable |

[Towards a Science of AI Agent Reliability](https://arxiv.org/abs/2602.16666) develops a reliability framework covering consistency, robustness, predictability, and safety. A benchmark's single success score cannot express all of these.

## Use graders appropriate to the outcome

- **Deterministic checks:** compare database state, receipts, schemas, or executable tests. These are strong when the intended result is precisely specified.
- **Model graders:** useful for nuanced qualities such as relevance, but calibrate them against human judgments, randomize comparison order, and test for verbosity and position bias.
- **Human review:** use for ambiguous cases, consequential mistakes, and grader calibration. Provide a rubric and measure disagreement.

Grade artifacts and effects as well as final messages. Record trajectories for diagnosis, but avoid penalizing every deviation from one reference path when multiple valid solutions exist. Keep judge inputs separate from untrusted agent text; agents must not be able to rewrite the grading policy.

## Repeated trials and fair comparisons

`pass@k` asks whether at least one of several attempts succeeds. It is useful only if a deployment can afford multiple attempts and select a good result. `pass^k` is often used for success across all k trials; state the exact estimator used by your benchmark. Under an illustrative independent-success model with probability `p`, these are `1 − (1 − p)^k` and `p^k`. Real trials may have correlated errors.

Report trial counts, uncertainty, and results by task category. Keep the task set and budgets comparable when changing a model or architecture. An agent with more samples, tools, or human assistance is a different system. Run ablations that change one major component at a time.

## Benchmark selection

These benchmarks cover complementary tasks and environments. Pin the version, split, harness, and permitted tools when comparing results.

| Benchmark | Useful for studying | Limitation to account for |
| --- | --- | --- |
| [SWE-bench Verified](https://www.swebench.com/verified) | Resolving repository issues with executable evaluation | Repository tasks do not cover the entire software lifecycle |
| [Terminal-Bench](https://www.tbench.ai/benchmarks) | Work in terminal environments | Version, sandbox resources, and harness configuration affect comparability |
| [τ²-bench](https://github.com/sierra-research/tau2-bench) | Tool use and user interaction in domain workflows | Simulated users and policies differ from your product |
| [OSWorld](https://osworld-v1.xlang.ai/) | Tasks in real computer environments | UI configuration, resets, and action latency matter |
| [GAIA](https://arxiv.org/abs/2311.12983) | General assistant tasks involving reasoning and tools | Dataset exposure and tool availability affect interpretation |
| [ClawBench](https://arxiv.org/abs/2604.08523) | Everyday tasks on live websites | Site drift and interception of final submissions affect reproducibility |
| [MultiAgentBench](https://arxiv.org/abs/2503.01935) | Collaboration and competition | Its coordination environments may not match your workflow |
| [PerspectiveGap](https://arxiv.org/abs/2606.08878) | Constructing multi-agent orchestration prompts | Pair this targeted capability probe with end-to-end application evaluation |
| [LoopsBench](https://arxiv.org/abs/2608.00267) | Long-running development with dependencies and regression obligations | Evaluate loop behavior as well as final task resolution |

## Turn evaluation into a release decision

Set thresholds before comparing candidates: required success by task category, prohibited effects, latency budget, and maximum cost. Track unknown or inconclusive results separately from accepted successes.

Use offline checks, then shadow or limited traffic, then broader rollout with rollback criteria. Inspect changes in task mix and tool availability before blaming the model. Export a small set of representative failure traces with sensitive data removed.

**Design question:** which final-state checks establish that a support refund used the correct amount, account, policy, and approval, and occurred exactly once?
