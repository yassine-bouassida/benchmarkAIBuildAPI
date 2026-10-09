# Experiment protocol — draft v0.1

## Research unit and scope
Each **run** is an independently initialized coding-agent session tasked with implementing one technology-neutral sports-community backend contract in a specific language/framework. A run is not one compiler invocation. The primary outcome is acceptance under a **predeclared fixed budget/termination policy**. Completion effort and runtime quality are secondary outcomes.

Candidates (proposed): Rust, Scala 3, C#/.NET, Python, JavaScript (Node.js), Java/JVM. Proposed frameworks must be declared before the experiment begins; framework selection is itself a confounder and should be reported explicitly.

## Conditions
- **Baseline:** identical neutral requirements, identical agent role/prompt shape, ordinary pinned development toolchains and allowed documentation, no curated language skill packages.
- **Enhanced:** same as baseline plus a versioned curated language-specific skill package. Record its exact contents, provenance and rationale.
- Compare across languages **within** a condition first. Compare the effect of skills **within** each language separately.
- Never call this a pure language-only comparison.

## Sequence
1. Design neutral functional spec, wire/API behavior, workload profiles, security expectations, and tests.
2. Select and document framework/toolchain/DB versions, shared PostgreSQL version, agent/model version, execution mode, permissions, network policy, and hardware. Provision and verify all toolchains, dependencies and equivalent environment images before measured coding begins; see environment-readiness.md.
3. Implement evaluator independently; freeze evaluation version/hash and hold out test scenarios.
4. Pilot each condition/candidate; fix measurement or ambiguous specification flaws and version changes before the main experiment.
5. Start each main run from an identical clean **language-specific starter**. If starter sizes vary, disclose exact boilerplate; consider a no-starter sensitivity test.
6. Assign randomized run order/identifiers; repeat ideally 5 times per language/condition (60 main runs if 6 languages x 2 conditions x 5 repetitions).
7. Stop according to predetermined policy; don't rescue failed runs by changing requirements.
8. Run functional tests and isolated performance tests. Aggregate by language/condition, show distributions and uncertainties, not one global score.

## Isolation
Each run has its own directory/repository clone, agent session and state, container or VM, database, caches, test namespace, credentials and logs. Worktrees only isolate files and are insufficient alone. Implementation agents must not access sibling code, branch histories, issue comments containing solutions, or post-run metrics. Restrict network and filesystem permissions accordingly.

## Model and effort
Keep agent model/configuration and prompt fixed within comparisons. Record reasoning/effort settings where available, retry/compaction events, interactive human guidance, and manual changes. Run-to-run context may vary; never represent deterministic equality. A comparable max token or wall-clock budget must be **measurable and enforceable**; otherwise report the constraint as approximate and avoid claiming strict parity.

## Scoring and fairness
Primary: independent functional/security/concurrency gate under prespecified limits. Secondary: completion rate, measured agent usage, time to verified completion, runtime performance, reliability, resource cost and maintainability audit. Compilation errors encountered are diagnostic metrics, **not** necessarily defects that persisted. Avoid pitting different levels of optimization or incompatible semantics against each other.

## Performance design
Use identical datasets, event/message distributions, hardware or dedicated instance class, database tuning, network topology, connection counts and warmup durations. Separate implementation runs from performance runs. Repeat measurements and randomize evaluation order. Report CPU, memory, DB metrics, throughput, p50/p95/p99 latency, failure rate, delivery/ordering semantics and tail behavior. Define SLO thresholds **before** testing, using a pilot calibration that is not scored.

## Publication
Publish prompts, manifests, tested commits, raw aggregate metrics and scripts where rights/privacy permit. Redact tokens, personal data and private agent traces. Publish failed runs and exclusions with reasons. Clearly label hypotheses, missing telemetry, protocol modifications, and threats to validity.

## Pending decisions
- Execution path for Codex subscription-supported CLI versus API, and whether usage events are available.
- Exact agent version/model, reasoning setting, prompt template, run budget and stop rules.
- Framework choices and dependency policies for Rust, Scala, C#, Python, JavaScript/Node.js and Java.
- API spec details and neutral WebSocket message protocol.
- Evaluator runner and load-generator language, anti-cheating boundary, hidden test design.
- Skill pack sourcing, audits and versioning.
- Hardware/cloud provider, concurrency and cost budgets.
- Statistical reporting approach and disclosures.
