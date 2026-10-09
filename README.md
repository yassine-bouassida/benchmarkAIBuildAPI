# AI Backend Build Benchmark

A public, reproducible experiment studying **AI-assisted backend engineering** in **Rust, Scala 3, and C# / ASP.NET Core**.

> **Status: methodology and specification draft — no language results, costs, or performance claims yet.**

## Research questions

1. How reliably does an AI coding agent implement the same realistic backend specification in each ecosystem?
2. How much agent effort, elapsed time, and measurable model usage does a correct implementation require?
3. What are the runtime latency, throughput, resource consumption, and reliability characteristics of completed implementations?
4. How does access to curated language-specific skills affect agent success and efficiency?

The subject is **the combination of model, tools, instructions, framework, and language**, not an intrinsic universal ranking of programming languages.

## Intended design

- Candidates: Rust, Scala 3, C#.
- Conditions: **baseline** (common instructions and standard toolchain/docs) and **skills-enhanced** (curated, versioned language-specific guidance).
- Pilot: one isolated run per candidate/condition before committing to a larger study.
- Main study (proposed): five independent runs per language/condition, conditional on pilot feasibility.
- All implementations meet the same externally specified observable behavior.
- Independent evaluator runs functional, adversarial, concurrency, and load tests.
- Unsuccessful, timed-out, and partial runs stay in the dataset.
- No performance benchmarks run on competing workloads simultaneously.

## Scope of the benchmark workload

A simplified sports community backend: private groups, multiple roles and permissions, events with capacity limits and FIFO waitlists, realtime channel messaging, persistence, and event notifications. This is **not** the production sports platform repository.

## Repository guide

- [AGENTS.md](AGENTS.md) — rules for any Codex/AI agent working here.
- [Experiment protocol](docs/experiment-protocol.md) — isolation, fairness, sampling, workflow.
- [Functional specification](docs/functional-spec.md) — required behavior and state transitions.
- [Evaluation plan](docs/evaluation.md) — gates, metrics, load tests, failure definitions.
- [Cost and telemetry](docs/cost-and-telemetry.md) — what we can and cannot measure.
- [Skill policy](docs/skills-policy.md) — baseline vs curated skills.
- [Codex handoff](prompts/codex-design-review.md) — first external design-review prompt.
- [Run manifest example](schemas/run-manifest.example.json) — reproducibility metadata.
- [Result example](schemas/run-result.example.json) — measurement output.

## Roadmap

1. **Design review**: critique and refine the protocol, API contract, evaluation, and costs.
2. **Implement neutral contracts and evaluator**; freeze a versioned acceptance suite before language implementations.
3. **Pilot** one independent run per candidate/condition, test telemetry and isolation.
4. **Main repetitions** using pinned model/toolchain/skills versions and resource constraints.
5. **Evaluate** on matched, isolated infrastructure; publish raw records, scripts, limitations, and aggregate statistics.

## Important constraints

Do not manufacture results or infer dollar cost from a flat subscription. ChatGPT/Codex or Claude subscriptions are **not interchangeable with separately billed APIs**. This experiment should be designed for subscription-supported interactive/CLI usage where permitted, without assuming that subscriptions provide an unrestricted programmatic agent-launch or usage-billing API. If cost/usage metadata is unavailable, report `null` with a reason.

Do not expose secrets, credentials, personal data, or private reasoning traces in a public repository. Do not silently change tests after viewing language results.

## Reproducing

This repository currently contains the **study design**, not a working benchmark runner. Runtime setup and commands will be documented after choosing a supported execution mechanism and implementing the test harness. No results are available yet.

## License / publication

License, citation metadata, and final disclosure policy must be selected before the first public benchmark results are published.
