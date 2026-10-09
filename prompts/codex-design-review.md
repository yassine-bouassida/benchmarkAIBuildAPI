# Codex task: critique and operationalize the benchmark design

You are acting as an **independent experimental-methodology reviewer** for the public AI Backend Build Benchmark.

Read: `README.md`, `AGENTS.md`, `docs/experiment-protocol.md`, `docs/functional-spec.md`, `docs/evaluation.md`, `docs/cost-and-telemetry.md`, `docs/skills-policy.md`, and example manifests.

**Do not launch benchmark runs or generate fake results.** We are at design stage.

Deliver:
1. An adversarial critique of confounders and unfair comparisons, ranked by severity.
2. A proposed *frozen* technology-neutral API and WebSocket contract plan.
3. A plan for independent evaluator and hidden tests; how to prevent implementation agents from changing evaluation criteria.
4. Feasible, subscription-compatible Codex run orchestration options without assuming API billing or unsupported CLI features. Identify what must be locally verified.
5. Versioned skill-pack plan for baseline/enhanced variants and impartial review criteria.
6. A minimal pilot protocol (1 run per language/condition), explicit stop rules and data collection plan.
7. An actionable GitHub issue breakdown with dependencies and acceptance criteria.
8. Publication, security, ethics, licensing, and reproducibility checklist.

State every assumption and verify toolchain/CLI capabilities from currently available documentation before claiming them. Any unknown usage metric must remain unknown. Propose edits by pull request rather than silently overwriting study assumptions. Ask for owner decision only on genuinely high-impact choices.
